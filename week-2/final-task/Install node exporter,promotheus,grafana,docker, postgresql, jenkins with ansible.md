# PENGINSTALLAN SEMUA APLIKASI WITH ANSIBLE

1. Install ansible

2. Membuat file bernama Inventory


        [all]
        103.183.75.150 ansible_user=sigit #monitoring
        103.172.205.236 ansible_user=sigit #app
        103.183.75.217 ansible_user=sigit
        103.179.57.187 ansible_user=sigit


        [app]
        103.172.205.236 ansible_user=app-sigit


        [monitoring]
        103.183.75.150 ansible_user=monitoring-sigit

        [gateway]
        103.183.75.217 ansible_user=sigit

        [jenkins]
        103.179.57.187

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/final-task/assets/a1.png)

3. membuat file keypem yang berisi id_rsa.pub 
4. membuat file ansible.cfg

       [defaults]
       inventory = Inventory
       private_key_file = key.pem
       command_warnings = false
       #host_key_checking = false
       timeout = 60

5. membuat file docker.yml yang berguna untuk install di semua server yang ada di inventory

6. membuat folder bernama files lalu buat file node-exporter.service, prometheus.service dan prometheus.yml ( yang digunakan untuk menargetkan ip yang akan di monitoring)

7. membuat file monitoring.yml yang nantinya akan di execute untuk server monitoring yang dimana akan tersintal , prometheus dan grafana

# Script monitoring on top docker

     - hosts: monitoring
       become: true
       gather_facts: yes
       tasks:
         - name: "copy configuration prometheus.yml"
             copy:
                  src: files/
                  dest: /home/sigit/prometheus/
                  owner: sigit
                  group: sudo
                  mode: 0664
         - name: "install prometheus"
           command: "docker run -d --name=prometheus -p 9090:9090 -v /home/sigit/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml prom/prometheus"
         - name: "install grafana"
           command: "docker run -d --name=grafana -p 3000:3000 grafana/grafana"'
      

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/final-task/assets/a2.png)




8. membuat file bernama file node-exporter.yml yg nanti akan di gunakan untuk install node-exporter di semua server

# Node exporter on top docker
Dengan cara 

     - hosts: gateway
       become: true
       gather_facts: yes
        tasks:
          - name: "install node exporter"
            command: "docker run -d --name=node-exporter --net=\"host\" --pid=\"host\" -v \"/:/host:ro,rslave\" prom/node-exporter:latest --path.rootfs=/host"

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/final-task/assets/a3.png)

9. jika semua sudah lihat node-exporter di port 9100

10. lalu jika sudah buka ip monitorinf di port 9090 untuk melihat prometheus

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/final-task/assets/a4.png)

11. dan buka ip main-sigit di port 3000 untuk membuka grafana

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/final-task/assets/a5.png)

# Cara  install docker di ansible
1. buat file bernama docker.yml
2. lalu masukan script


       - hosts: all
         become: yes
           tasks:
          - name: 'update'
            apt:
             update_cache: yes

          - name: 'upgrade'
            apt:
             upgrade: yes

          - name: 'install docker depedencies'
            apt:
               name:
                 - ca-certificates
                 - curl
                 - gnupg
                 - lsb-release

          - name: 'add docker url'
            apt_key:
                url: https://download.docker.com/linux/ubuntu/gpg 

          - name: 'add repo'
            apt_repository:
                repo: deb https://download.docker.com/linux/ubuntu focal stable
                state: present

          - name: 'docker install'
            apt:
               name: 
                 - docker-ce
                 - docker-ce-cli
                 - containerd.io

          - name: 'docker compose install'
            shell: sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

          - name: 'set permission docker-compose'
            shell: sudo chmod +x /usr/local/bin/docker-compose

          - name: 'setup docker command without sudo'
            shell: sudo usermod -aG docker sigit

3. runing dengan ansible-playbook docker.yml

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/final-task/assets/a6.png)

# Cara install jenkins with ansible on top docker
1. buat file bernama jenkins.yml
2. masukan script
 
  - hosts: jenkins
  become: true
  gather_facts: yes
  tasks:
    - name: "run container jenkins"
      command: "docker run -u 0 --name jenkins -p 8080:8080 -p 50000:50000 -d --restart always -v /home/sigit/jenkins_home:/var/jenkins_home jenkins/jenkins"


3. runing dengan ansible-playbook jenkins.yml

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/final-task/assets/a7.png)


# Cara install postgresql on top docker
1. buat file bernama postgre.yml
2. masukan script 


        - hosts: app
          become: true
          gather_facts: yes
            tasks:
                   - name: "postgresql with docker"
                     command: docker run --name postgresql -e POSTGRES_USER=sigit -e POSTGRES_DB=dumbflix -e POSTGRES_PASSWORD=Sotoy123 -p 5432:5432 -v /home/sigit/postgres:/var/lib/postgresql/data -d postgres

3. jalankan dengan ansible-playbook postgre.yml


![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/final-task/assets/a8.png)


# Cara Create User ke semua server with ansible
1. buat file bernama create-user.yml
2. install whois untuk generate password menjadi token
( sudo apt install whois )
3. mkpasswd --sha-512
4. masukan password yg di inginkan
5. jika sudah muncul token copy token tersebut lalu nanti paste di script create.user.yml
6. masukan script


       -hosts: all
        become: yes
        tasks:
        - name: 'create user'
          user:
               name: sigit
               password: $6$2/HUl4sX9UN$b7teicKG29cMnIsPk4RcA5EVXEX1il4CqbmMZNGuohGhcCbKUGSyvUJreK/3GhQLqlL3PvNknIvs1xiHr2n.s/
               groups: sudo
               state: present
               shell: /bin/bash
               system: no
               createhome: yes
               home: /home/sigit

        - name: 'change pw'
          lineinfile:
                path: /etc/ssh/sshd_config
                regexp: 'PasswordAuthhentication no'
                line: PasswordAuthentication yes
        
        - name: 'reload ssh'
          systemd:
               name: sshd
               state: reloaded               

7. ansible-playbook create-user.yml

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/final-task/assets/a9.png)

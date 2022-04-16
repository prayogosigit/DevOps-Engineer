1. Instal docker & docker-compose di server aplikasi, dengan cara 

sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io

sudo usermod -aG docker app-sigit

sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose



2. Clone aplikasi backend dan frontend
3. buat frontend mengenali backend ( `scr/config/api.js`) tambahakan ip backend
4. install mysql di dalam docker ( docker pull mysql )
5. Selanjutnya jadikan mysql menjadi container
CARA 1:
membuat kontener mysql dengan volume ( `docker container create --name database -p 3306:3306 -v ~/mysql-data:/var/lib/mysql mysql:latest` 

CARA 2:
( `docker run -d --name database -p 3306:3306 -v ~/mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=Sotoy123 -e MYSQL_DATABASE=wayshub mysql:latest` )

6. masuk ke container mysql ( `docker exec -it database bash` )
** database adalah nama kontener untuk mysql88
7. masuk ke direktori ( `cd var/lib/mysql` )
8. login mysql dengan cara
       ( `mysql -u root -p` ) 
9. use wayshub;
10. Langkah selanjutnya setting config agar aplikasi frontend mengenali backend, dengan cara
           1. masuk ke direktori frontend
           2. masukan perintah `sudo nano /src/config/api.js`
           3. lalu ubah baseurl nya dengan ip backend dan portnya atau domain yg sudah di konfigurasi
           4. ( baseURL: "https://api.sigit.studentdumbways.my.id/api/v1" )
11. Langkah selanjutnya seting congit agar backend mengenali database. dengan cara :
           1. masuk ke direktori backend
           2. masuk ke `sudo nano /config/config.json`
           3. pada kolom development
------------------------------------------
"username": "root",
    "password": "Sotoy123",
    "database": "wayshub",
    "host": "103.172.205.236",
    "dialect": "mysql"
---------------------------------------------

11. Lakukan konfigurasi di server nginx pertama buat reverse proxy dengan cara:
        1. buat folder di `etc/nginx/`
        2. lalu buat folder bernama revproxy
        2. lalu buat file bernama backend yang isi nya ip dari server backand dengan port
---------------------------------------------------------------             
server {
    server_name api.sigit.studentdumbways.my.id;

    location / {
             proxy_pass http://103.226.138.182:5555;
    }
}    
--------------------------------------------------------------    

         3. lalu buat file 1 lagi untuk membuat reverser proxy aplikasi frontend dengan nama file frontend dengan memasukan ip public frontend
-----------------------------------------------------------------
server {
    server_name front.sigit.studentdumbways.my.id;

    location / {
             proxy_pass http://103.226.138.182:3000;
   
    }
}
----------------------------------------------------------------

          4. Setelah itu lakuakn konfigurasi pada file nginx.conf yang berlokasi
          di `cd /etc/nginx/nginx.conf` Setting di bagian include nya memasukan lokasi dari file reverse proxy yg tadi di buat
          ( include /etc/nginx/revproxy/*; )
          5. langkah terkahir restart nginx dengan cara ( sudo systemctl restart
           nginx )

10. selanjtunya membuat aplikasi Backend menjadi image di docker
       -dengan cara 
           1. masuk ke direktori backend 
           2. membuat file dengan nama Dockerfile
           3. membuat srcipt
           4. FROM node:latest
               WORKDIR /usr/app
               COPY . .
               RUN npm install
               RUN npm install sequelize-cli -g
               RUN npx sequelize db:migrate
               EXPOSE 5000
               CMD [ "npm", "start" ]
11. jangan lupa copy env.example menjadi .env
12. setelah itu build Docker file dengan cara 
        ( docker build -t sigit/ways-be:2.0 .)
13. setelah menjadi docker images jalankan menjadi container dengan cara
        ( docker run -d --name be -p 5000:5000 sigit26/ways-be:2.0 )
14. Langkah selanjutnya meng push images backend ke docker hub dengan cara
       1. login docker (masukan username dan password) usernameny =sigit26
       2. docker tag sigit/ways-be :2.0 sigit26/ways-be:2.0
       3. docker push sigit26/ways-be:2.0

15. lakukan build aplikasi frontend dengan cara:
       1. membuat file bernama Dockerfile di direktori frontend
       2. isi dari dockerfile sebagai berikut, lalu save.
((((((((((((((
FROM node:10
WORKDIR /usr/src/app
COPY . .
RUN npm install
EXPOSE 3000
CMD [ "npm", "run", "start" ] 
))))))))))))))))))

      3. lalu jalankan perintah untuk membuat menjadi images( docker build -t sigit26/ways-fe:2.0 )
      4. Langkah selanjutnya meng push images Frontend ke docker hub dengan cara
       1. login docker (masukan username dan password) usernameny =sigit26
       2. docker tag `sigit/ways-fe :1.0 sigit26/ways-be:2.0` ( untuk merubah nama image )
       3. docker push `sigit26/ways-be:2.0`

16. Langkah selanjutya install docker-compose dengan cara
      1. ( sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose )

      2. ( sudo chmod +x /usr/local/bin/docker-compose )

17. Langkah selanjutnya buat file dengan nama docker-compose.yml yang berisi
      1. 
(((((((((((((((((((((
version: '3.7'
services:
        frontend:
          container_name: fe
          image: sigit26/ways-fe:1.0
          stdin_open: true
          ports:
            -  "3000:3000"
)))))))))))))))))))))
      2. lalu jalankan file docker-compose.yml nya dengan cara ( docker-compose up -d )

14. Langkah selanjutnya konfigurasi domain agar menjadi ssl dengan cara
        1. lakukan konfigirasi pada DNS di cloudflare dengan cara membuat subdomain untuk aplikasi backend = api.sigit.studentdumbways.my.id dan proxy di off kan dan front.sigit.studentdumbways.my.id .
        2. Langkah selanjutnya membuat doamin tersebut menjadi https
               1. install cerbot ( sudo apt install certbot python3-certbot-nginx )
               2. sudo certbot --nginx -d api.sigit.studentdumbways.my.id
               3. masukan email kamu
               4. lalu pilih angka 2 untuk redirect otomatis
               5. setelah coba masukan domain di web browser tadda bisa
               6. lakukan untuk frontend sudo certbot --nginx -d front.sigit.studentdumbways.my.id

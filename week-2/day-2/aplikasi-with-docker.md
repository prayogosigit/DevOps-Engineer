1. Instal docker & docker-compose di server aplikasi, dengan cara 

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/a1.png)


2. Clone aplikasi backend dan frontend
3. buat frontend mengenali backend ( `scr/config/api.js`) tambahakan ip backend
4. install mysql di dalam docker ( docker pull mysql )

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/a2.png)

5. Selanjutnya jadikan mysql menjadi container


CARA 1:
membuat kontener mysql dengan volume ( `docker container create --name database -p 3306:3306 -v ~/mysql-data:/var/lib/mysql mysql:latest` 

CARA 2:
( `docker run -d --name database -p 3306:3306 -v ~/mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=Sotoy123 -e MYSQL_DATABASE=wayshub mysql:latest` )

6. masuk ke container mysql ( `docker exec -it database bash` )

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/a3.png)

### database adalah nama kontener untuk mysql
7. masuk ke direktori ( `cd var/lib/mysql` )
8. login mysql dengan cara
       ( `mysql -u root -p` ) 
9. ketik `use wayshub;`
10. Jika sudah exit dengan CTRL+ D
11. Langkah selanjutnya setting config agar aplikasi frontend mengenali backend, dengan cara
           
           1. masuk ke direktori frontend
           
           2. masukan perintah `sudo nano /src/config/api.js`
           
           3. lalu ubah baseurl nya dengan ip backend dan portnya atau domain yg sudah di konfigurasi
           
           4.( baseURL: "https://api.sigit.studentdumbways.my.id/api/v1" )
 
 
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/a4.png)
 
12. Langkah selanjutnya seting config agar backend mengenali database. dengan cara :
           
           1. masuk ke direktori backend
           2. masuk ke `sudo nano /config/config.json`
           3. pada kolom development

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/a5.png)

11. Lakukan konfigurasi di server nginx pertama buat reverse proxy dengan cara:
        
        1. buat folder di etc/nginx/
        2. lalu buat folder bernama revproxy

11.1 lalu buat file bernama backend yang isi nya ip dari server backand dengan 
       
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/a6.png)

12. lalu buat file 1 lagi untuk membuat reverser proxy aplikasi frontend dengan nama file frontend dengan memasukan ip public frontend

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/a7.png)

   4. Setelah itu lakuakn konfigurasi pada file nginx.conf yang berlokasi
          di `cd /etc/nginx/nginx.conf` Setting di bagian include nya memasukan lokasi dari file reverse proxy yg tadi di buat
          ( `include /etc/nginx/revproxy/*;` )
          
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/a8.png)

   5. langkah terkahir restart nginx dengan cara ( sudo systemctl restart nginx )

10. selanjtunya membuat aplikasi Backend menjadi image di docker,dengan cara: 
           
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
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/a9.png)

11. jangan lupa copy env.example menjadi .env
12. setelah itu build Docker file dengan cara 
         `docker build -t sigit/ways-be:2.0 .`
13. setelah menjadi docker images jalankan menjadi container dengan cara
        `docker run -d --name be -p 5000:5000 sigit26/ways-be:2.0`
14. Langkah selanjutnya push images backend ke docker hub dengan cara
       
        1. login docker (masukan username dan password) usernameny =sigit26
        2. docker tag sigit/ways-be :2.0 sigit26/ways-be:2.0
        3. docker push sigit26/ways-be:2.0
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/a10.png)

15. lakukan build aplikasi frontend dengan cara:
        
        1. membuat file bernama Dockerfile di direktori frontend
        2. isi dari dockerfile sebagai berikut, lalu save.
       
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/a11.png)

15. lalu jalankan perintah untuk membuat menjadi images
`docker build -t sigit/ways-fe:2.0 .`

16. Langkah selanjutnya meng push images Frontend ke docker hub dengan cara
17. `login docker` (masukan username dan password) usernameny =sigit26
18. `docker tag sigit/ways-fe :1.0 sigit26/ways-be:2.0` ( untuk merubah nama image )
19. `docker push sigit26/ways-be:2.0`

20. Langkah selanjutnya buat file dengan nama docker-compose.yml di direktori Frontend-Wayshub yang berisi
   
`version: '3.7'
services:
        frontend:
          container_name: fe
          image: sigit26/ways-fe:1.0
          stdin_open: true
          ports:
            -  "3000:3000"`

21. lalu jalankan file docker-compose.yml nya dengan cara `docker-compose up -d` 

## Langkah selanjutnya konfigurasi domain agar menjadi ssl dengan cara
1. lakukan konfigirasi pada DNS di cloudflare dengan cara membuat subdomain untuk aplikasi backend = api.sigit.studentdumbways.my.id dan proxy di off kan dan front.sigit.studentdumbways.my.id

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/a12.png)

## Langkah selanjutnya membuat doamin tersebut menjadi https

1. install cerbot `sudo apt install certbot python3-certbot-nginx`
2. Lakukan perintah untuk membuat cartificat
3. `sudo certbot --nginx -d api.sigit.studentdumbways.my.id`
4. masukan email kamu
5. lalu pilih angka 2 untuk redirect otomatis
6. setelah coba masukan domain di web browser tadda bisa
7. lakukan untuk frontend sudo certbot --nginx -d front.sigit.studentdumbways.my.id

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/a13.png)

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/a14.png)

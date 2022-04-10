
# Deploy Frontend & Backend

* Persiapkan aplikasi frontend dan backend
**frontend**
```sh
git clone https://github.com/rioprayogo/wayshub-frontend.git
```
**backend**
```sh
git clone https://github.com/rioprayogo/wayshub-backend.git
```
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/a1.png)

* Instal

* Persiapkan engine untuk menjalankan aplikasi
**nvm**
```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```
 ![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/a2.png)

 * Jika sudah lakukan 'nvm install 16' untuk menginstall nvm versi 16 pada frontend dan backend dan lakukan `exec bash` untuk me refresh nvm agar terbaca

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/a3.png)
 
 * Jika sudah masuk ke server Database untuk setting database dengan menggunakan
'''sh
sudo apt install mysql-server
'''
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/d1.png)

 * Selanjutnya lakukan konfigursi untuk membuat server agar bisa menggunakan pasword, kekuatan password dan permision lainnya. seperti Permintaan apakan bisa remote server? apakah bisa untuk menghapus user test anoymouse?dlldengan cara
'''sh
sudo mysql_secure_installation
'''
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/d2.png)

 * Lalu kita masuk ke dalam database sql dengan menggunakan perintah tersebut

'''shsh
mysql -u root -p
'''

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/d3.png)

* Langkah selanjutnya kita membuat user baru dengan cara 

'''sh
CREATE USER 'sigit'@'%' IDENTIFIED BY 'Sotoy123';
'''

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/d4.png)

`keterangan di atas menunjukan sigit=username | Sotoy123=password`

 * Lalu selanjutnya membuat database dengan cara 

'''sh
CREATE DATABASE wasyhub;
'''

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/d5.png)

'keterangan di atas kita membuat database dengan nama wayshub'

 * Untuk memastikan database berhasil di buat kita bisa memberikan perintah
'''sh
SHOW DATABASES;
'''
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/d6.png)

untuk melihat isi database 

'''sh
SHOW TABLES;
'''

 * Selanjutnya untuk membuat database agar bisa di akses dengan user sigit ketik perintah

'''sh
GRANT ALL PRIVILAGES ON wayshub.* TO 'sigit'@'%';
'''

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/d7.png)

lalu

'''sh
FLUSH PRIVILEGES;
'''
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/d8.png)

 * Setelah semua terbuat saatya kita login menggunkan user baru yang tadi di buat, dengan cara 

'''sh
mysql -u sigit -p
'''
lalu lakukan `SHOW DATABASES;` dan `use wayshub` untuk menggunakan database wayshub

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/d9.png)

 * Setelah semua sudah terkonfigurasi di mysql, lakukan konfigurasi di server database dengan
`sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf`
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/d10.png)

## Langkah selanjutnya
### Konfigurasi di server aplikasi dir frontend
 
 * Lakukan config `sudo nano /frontend/src/config/api.js` pada frontend agar dapat terhubung dengan backend
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/a16.png)
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/a17.png)

### Konfigurasi di server aplikasi dir backend

* Lakukan config `sudo nano /backend/config/config.json` pada backend agar dapat tehubung dengan database
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/a12.png)
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/a13.png)
* Selanjutnya copy env.example menjadi .env
`cp env.example .enc`
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/a11.png)

* Install sequleize yang berfungsi memetakan data untuk migrasi ke database
**install sequelize**
```sh
npm install sequelize-cli -g
```
**untuk menjalankan sequelize**
```sh
npx sequelize db:migrate
```
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/a14.png)
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/a15.png)

* Gunakan pm2 agar aplikasi dapat berjalan di background install pm2 dan setting di kedua direktori backend dan frontend
**untuk mendownload pm2**
```sh
npm install pm2
```
* Jalankan dan configurasikan pm2 dengan `pm2 ecosystem simple` dan `pm2 start` untuk mendapatkan file ecosystem.config.js dan menjalankanya
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/a18.png)
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/a19.png)

* lalu masuk dan edit file `ecosystem.config.js`
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/a20.png)
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/a21.png)

* Terakhir untuk menjalan kan aplikasi pada kedua direktori frontend dan backend meggunakan
'''sh
pm2 start ecosystem.config.js
'''
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/a24.png)
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-1/assets/a25.png)

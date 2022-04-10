
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
aaa1

* Instal

* Persiapkan engine untuk menjalankan aplikasi
**nvm**
```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```
 aaa2

 * Jika sudah lakukan 'nvm install 16' untuk menginstall nvm versi 16 pada frontend dan backend dan lakukan `exec bash` untuk me refresh nvm agar terbaca

aaaa3
 
 * Jika sudah masuk ke server Database untuk setting database dengan menggunakan
'''sh
sudo apt install mysql-server
'''
aaaD1

 * Selanjutnya lakukan konfigursi untuk membuat server agar bisa menggunakan pasword, kekuatan password dan permision lainnya. seperti Permintaan apakan bisa remote server? apakah bisa untuk menghapus user test anoymouse?dlldengan cara
'''sh
sudo mysql_secure_installation
'''
aaaD2

 * Lalu kita masuk ke dalam database sql dengan menggunakan perintah tersebut
'''sh
mysql -u root -p
'''
AAD3

* Langkah selanjutnya kita membuat user baru dengan cara 
'''sh
CREATE USER 'sigit'@'%' IDENTIFIED BY 'Sotoy123';
'''
aaaD4

`keterangan di atas menunjukan sigit=username | Sotoy123=password`

 * Lalu selanjutnya membuat database dengan cara 
'''sh
CREATE DATABASE wasyhub;
'''
aaaD5

'keterangan di atas kita membuat database dengan nama wayshub'

 * Untuk memastikan database berhasil di buat kita bisa memberikan perintah
'''sh
SHOW DATABASES;
'''
aaaD6
untuk melihat isi database 
'''sh
SHOW TABLES;
'''

 * Selanjutnya untuk membuat database agar bisa di akses dengan user sigit ketik perintah
'''sh
GRANT ALL PRIVILAGES ON wayshub.* TO 'sigit'@'%';
'''
aaaD7

lalu
'''sh
FLUSH PRIVILEGES;
'''
AAD8

 * Setelah semua terbuat saatya kita login menggunkan user baru yang tadi di buat, dengan cara 
'''sh
mysql -u sigit -p
'''
lalu lakukan `SHOW DATABASES;` dan `use wayshub` untuk menggunakan database wayshub

aad9

 * Setelah semua sudah terkonfigurasi di mysql, lakukan konfigurasi di server database dengan
`sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf`
aaad10

## Langkah selanjutnya
### Konfigurasi di server aplikasi dir frontend
 
 * Lakukan config `sudo nano /frontend/src/config/api.js` pada frontend agar dapat terhubung dengan backend
 aa16
 aa17

### Konfigurasi di server aplikasi dir backend

* Lakukan config `sudo nano /backend/config/config.json` pada backend agar dapat tehubung dengan database
aa12
aa13
* Selanjutnya copy env.example menjadi .env
`cp env.example .enc`
aa11

* Install sequleize yang berfungsi memetakan data untuk migrasi ke database
**install sequelize**
```sh
npm install sequelize-cli -g
```
**untuk menjalankan sequelize**
```sh
npx sequelize db:migrate
```
aa14
aa15

* Gunakan pm2 agar aplikasi dapat berjalan di background install pm2 dan setting di kedua direktori backend dan frontend
**untuk mendownload pm2**
```sh
npm install pm2
```
* Jalankan dan configurasikan pm2 dengan `pm2 ecosystem simple` dan `pm2 start` untuk mendapatkan file ecosystem.config.js dan menjalankanya
aa18
aa19
* lalu masuk dan edit file `ecosystem.config.js`
aa20
aa21

* Terakhir untuk menjalan kan aplikasi pada kedua direktori frontend dan backend meggunakan
'''sh
pm2 start ecosystem.config.js
'''

aa24
aa25
# Langkah 1
## Reverse Proxy

1. Pertama-tama kita buat setiing untuk reverse proxynya dulu dengan masuk ke folder nginx setelah itu buat suatu directory baru telebih dahulu.

cd /etc/nginx

a

2. lalu membuat folder baru dengan mengetik sudo mkdir dumbways
3. Setelah itu masuk ke directory yang sudah dibuatsetelah itu buat suatu file dengan nama my.reverse-proxy.conf

a

--Setelah itu masukkan konfigurasi berikut:

a

4. ika sudah simpan konfigurasi.

Selanjutnya keluar dari directory dumbways, setelah itu masuk ke dalam file nginx.conf.

sudo nano nginx.conf

a

5. kemudian pastikan untuk melakukan pengecekan konfigurasi dengan menjalankan perintah :

sudo nginx -t

a

6. Jika sudah sekarang kita tinggal melakukan restart/reload Nginx kita.

sudo systemctl restart nginx

a


7. skarang kita akan membuat sebuah virtual host. Untuk membuat virtual host kita harus masuk ke local server kita setelah itu masuk ke dalam file /etc/hosts.

sudo nano /etc/hosts
-- lalu ketikan ip kalian dan domain kalian seperti berikut

a

8. Jika sudah sekarang coba buka web browser kalian setelah itu coba akses nama domain kalian.

a

9. Jika kita lihat disini adalah kita mendapatkan 502 Bad Gateway kenapa? karena kita belum menjalankan aplikasi kita.
Sekarang kita coba untuk menjalankan aplikasi dumbflix yang sudah pernah kita pakai sebelumnya.
Untuk menjalankan aplikasi dumbflix kalian dapat mengikuti langkah-langkah berikut.

-- git clone https://github.com/dumbwaysdev/dumbflix-frontend.git
-- cd dumbflix-frontend
-- npm install 

a

-- npm start

a



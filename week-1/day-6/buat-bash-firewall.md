# Langkah 1

1. Pastikan sudah instal firewallnya dengan cara (sudo apt install ufw -y)

a

2. Lalu buatlah file yang ber extension .sh

a

3. masukan script di file tersebut dengan cara (sudo nano [namafiletsb])

a

masukan teks ini

#!/bin/bash

sudo ufw allow 22;sudo ufw allow 80;sudo ufw allow 443

a

4. lalu kalian check apaka file tersebut sudah bisa di excute? jika belum lakukan perintah

(chmod u+x [namafilenya])

5. jika sudah akan berwarna hijau seperti gambar di bawah

a

6. untuk menjalankan file tersebut ketik (./namafile)

a


7. tada berhasil di jalankan


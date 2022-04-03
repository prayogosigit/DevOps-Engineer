# Langkah 1

1. Pastikan sudah instal firewallnya dengan cara (sudo apt install ufw -y)

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-6/assets/7.png)

2. Lalu buatlah file yang ber extension .sh

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-6/assets/8.png)

3. masukan script di file tersebut dengan cara (sudo nano [namafiletsb])

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-6/assets/9.png)

masukan teks ini

#!/bin/bash

sudo ufw allow 22;sudo ufw allow 80;sudo ufw allow 443

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-6/assets/10.png)

4. lalu kalian check apaka file tersebut sudah bisa di excute? jika belum lakukan perintah

(chmod u+x [namafilenya])



![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-6/assets/11.png)

5. jika sudah akan berwarna hijau seperti gambar di bawah

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-6/assets/12.png)

6. untuk menjalankan file tersebut ketik (./namafile)

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-6/assets/13.png)


7. tada berhasil di jalankan

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-6/assets/14.png)

# Langkah 1
## Langkah awal adalah mendownload Ubuntu server dan Aplikasi VMware
 1. Buka link "https://ubuntu.com/download/server" dan klik "Option 2 - Manual server installation"
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/11.png)
 2. Download aplikasi VMware di 'https://www.vmware.com/products/workstation-player/workstation-player-evaluation.html'
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/22.png)
# Langkah 2
## Install dan Setup VMware
 1. Buka Virtual machine VMware. lalu klik di bagian Create a new Virtual Machine.
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/1.png)
 2. Lalu pilih saja di bagian use ISO image. Setelah itu masuk ke bagian browser lalu cari lokasi ISO ubuntu server yang sudah di download.


![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/2.png)

 3. Masukan user dan password yang kalian inginkan.


![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/3.png)

4. Lalu tentukan lokasi dimana Virtual machine kalian ingin disimpan.
5. dan atur size disk yang ingin kalian gunakan. Disini sebagai contoh saya menggunakan 10GB. lalu klik next

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/4.png)

6. Setelah itu Pilih "Customize Hardware" untuk mengkonfigurasi Virtual Machine Ubuntu Server kita

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/5.png)

7. Kemudian pada bagian Network Adapter pilih "NAT" kemudian close. Lalu Finish

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/6.png)

8. Jika sudah nanti akan arahkan ke bagian installasi, disini tunggu saja sampai prosesnya selesai. ketika selesai akan muncul tampilan seperti gambar dibawah ini. Setelah itu pilih bahasa yang ingin digunakan English.

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/7.png)

9. Pada proses saat ini bisa di skip dengan klik done

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/8.png)

10. Lalu pilih di bagian ens33, dan setelah itu pada bagia IPv4 Method ubah dari yang awalnya automatic menjadi manual. Setelah itu masukan detail IP (untuk mengubah menjadi ip DHCPv4 menjadi statis)

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/99.png)


![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/10.png)


11. Saat ini IP sudah menjadi statis

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/111.png)

12. Lalu skip dengan klik Done.

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/33.png)

13. Nah di bagian ini kita pilih Custom storage layout. Lalu klik Done.

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/44.png)

14. Selanjutnya di local disk pilih Add GPT Partition.

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/55.png)

15. Di bagian ini masukan saja size yang maksimal. Lalu klik Create


![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/66.png)

15. Selanjutnya tampilanya akan seperti di bawah ini. Lalu klik Done


![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/77.png)

16. Lalu akan muncul notifikasi untuk mengkonfirmasi semua konfigurasi yang sudah kita buat. Jika sudah langsung klik saja Continue.

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/999.png)

17. Untuk membuat profile kita isi nama dan pasword sesuai form yang di tampilkan

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/100.png)

18. Lalu checklist bagian Install OpenSSH server yang nantinya berguna untuk meremote server

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/101.png)

19. Pada tahap ini langsung saja klik done 

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/102.png)

20. tunggu beberapa saat proses intalasi jika sudah klik Reboot Now

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/103.png)

21. Nah jika sudah masukan ID dan pasword yang tadi sudah di daftarkan

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-1/assets/104.png)


























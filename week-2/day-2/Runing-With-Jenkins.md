1. install jenkins. dengan cara 
       
       1. sudo apt install openjdk-11-jdk
       2. wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
       3. sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
       4. sudo apt update
       5. sudo apt install jenkins
      
2. Konfigurasi DNS. (buat sub domain untuk jenkin)

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/j1.png)

3. masuk ke server nginx

4. lakukan reverse proxy

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/j2.png)

5. restart nginx

6. Selanjutnya ubah domain http menjadi https dengan cara:
        
        1. ( sudo certbot --nginx -d jenkins.sigit.studentdumbways.my.id )
        2. lalu pilih 2 untk install secaara otomatis direct

7. jika sudah masuk ke domain jenkins.sigit.studentdumbways.my.id

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/j3.png)

8. pada saat diawal kita di minta untuk memasukan key yg terdapat di lokasi penginstallan jenkiins

9. Selanjutnya membuat username dan password untuk login jenkins

10. Tahap selanjutnya penginstallan secara otomatis untuk yg di perlukan (pilih saja suggest installaiton)

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/j4.png)

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/j5.png)

11. jika sudah masuk ke dashbord install plugin dlu yaitu ( `ssh agent` ) 

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/j6.png)

12. nah jika sudah finish tahaap selanjutnya membuat credensial terlebih dahulu. dengan cara 
         
         1. klik manage jenkins
         2. klik manage credensial
         3. di bawah tulisan global klik tanda panah lalu pilih add
         4. lalu isi username dengan ( Server )
         5. lalu id masukan dengan nama server aplikasi ( app-sigit1)
         6. lalu di bagian private key masukan dari rsa_id server aplikasi
         7. jangan lupa rsa_id.pub nya di copy ke autorize-keysnya
 ![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/j7.png)
 ![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/j8.png)

13. Selanjutnya membuat job dengan cara
         
         1. pilih new item 
         2. nah beri nama 
         3. lalu pilih pipeline
         4. padah kolom Build Trigger centang bagian ( Github hook triger )
         5. pada kolom pipleline pilih ( Pipeline script for SCM )
         6. pada kolom SCM pilih ( Git )
         7. Selanjutnya masukan repository URL nya dengan http dri repo frontend
         8.  lalu masukan credential yang tadi kita buat yaitu ( Server )
         9.  lalu pilih branchnya "main" ya karna reporsitorynya berada di branch main
         10. lalu pilih apply dan save
 ![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/j9.png)
 ![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/j10.png)
 

14. Selanjutnya kita masuk ke github untuk mengaktifkan webhooknya dengan cara:
          
          1. masuk ke repository tersebut (Frontend- Wayshub) pilih setting
          2. pilih webhook
          3. lalu klik add webhook
          4. lalumasukan dari url jenkins yg di ikuti /github-webhook/
          5. ( https://jenkins.sigit.studentdumbways.my.id/github-webhook/ )
          6. lalu save
![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/j11.png)

15. tahap selanjutnya membuat file pipeline di direktori Frontend yang bernana ( Jenkinsfile ). Yang isinya :

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-2/day-2/assets/j12.png)

16. langkah selanjutnya push semua file yg ada di Direktori Frontend-Wayshub
17. setelah done coba buat update pada github repo tsb.

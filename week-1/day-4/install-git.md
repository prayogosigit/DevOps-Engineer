# Langkah 1

1. Install git dengan cara ketik "sudo apt install git"

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-4/assets/1.png)

2. git config --global user.name "your.github-user.name" dan git config --global user.email "your.github-user.email" untuk menerapkan id dan email user

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-4/assets/2.png)

4. ketik ssh-keygen lalu enter enter hinga muncul seperti berikut

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-4/assets/3.png)

5. cat .ssh/id_rsa.pub copy script dari situ lalu paste di file .ssh-rsa

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-4/assets/5.png)

6. lalu paste lagi di github kalian dan pilih new ssh keys (https://github.com/settings/keys.)

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-4/assets/4.png)

7. lalu ketikan pertintah ssh -T git@github.com

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-4/assets/7.png)

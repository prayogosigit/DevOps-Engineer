# Langkah 1

1. Install git dengan cara ketik "sudo apt install git"



2. git config --global user.name "your.github-user.name" dan git config --global user.email "your.github-user.email" untuk menerapkan id dan email user



4. ketik ssh-keygen lalu enter enter hinga muncul seperti berikut



5. cat .ssh/id_rsa.pub copy script dari situ lalu paste di file .ssh-rsa



6. lalu paste lagi di github kalian dan pilih new ssh keys (https://github.com/settings/keys.)



7. lalu ketikan pertintah ssh -T git@github.com

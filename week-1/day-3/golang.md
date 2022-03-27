# Langkah 1

1. Pertama-tama sama seperti sebelumnya, kita harus mendownload engine-nya terlebih dahulu. dengna mengetik
"wget https://golang.org/dl/go1.16.5.linux-amd64.tar.gz && sudo su"

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-3/assets/10.png)

2. lalu ketik "rm -rf /usr/local/go && tar -C /usr/local -xzf go1.16.5.linux-amd64.tar.gz && exit"

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-3/assets/10.png)

3. Selanjutnya masukkan path go pada .bashrc dengan mengetik "sudo nano .bashrc"



4. masukan kode berikut "export PATH=$PATH:/usr/local/go/bin"



5. setelah itu perika versi kamu dengan mengetik "go version"

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-3/assets/11.png)

6. lalu buat file index.go dan masuk script berikut


package main


import "fmt"

func main() {
    fmt.Println("Hello World!")
}

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-3/assets/17.png)

7. Sekarang jalankan aplikasi go dengan menggunakan perintah berikut "go run index.go"

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-3/assets/14.png)

8. lalu build dengan perintah ""go build index.go"

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-3/assets/15.png)

9. jika sudah masukan perintah tersebut dengan mengetik "./index"

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-3/assets/16.png)

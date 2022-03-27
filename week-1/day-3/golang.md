# Langkah 1

1. Pertama-tama sama seperti sebelumnya, kita harus mendownload engine-nya terlebih dahulu. dengna mengetik
"wget https://golang.org/dl/go1.16.5.linux-amd64.tar.gz && sudo su"

a

2. lalu ketik "rm -rf /usr/local/go && tar -C /usr/local -xzf go1.16.5.linux-amd64.tar.gz && exit"

a

3. Selanjutnya masukkan path go pada .bashrc dengan mengetik "sudo nano .bashrc"

a

4. masukan kode berikut "export PATH=$PATH:/usr/local/go/bin"

a

5. setelah itu perika versi kamu dengan mengetik "go version"

a

6. lalu buat file index.go dan masuk script berikut
package main

import "fmt"

func main() {
    fmt.Println("Hello World!")
}

6. Sekarang jalankan aplikasi go dengan menggunakan perintah berikut "go run index.go"

a

7. lalu build dengan perintah ""go build index.go"

a

8. jika sudah masukan perintah tersebut dengan mengetik "./index"

a

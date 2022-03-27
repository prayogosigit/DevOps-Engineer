# Langkah 1
1. Pertama-tama kita harus meng-install terlebih engine-nya dahulu. dengan cara "curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash"

a

2. jika NVM belum terdekteksi ketik "exec bash" untuk me refresh

a


4. Selanjutnya lakukan peng installan dengan keltik "nvm install 16" untuk nvm versi 16

a

5. untuk menggunakan nvm versin 16 ketik "nvm use 16" dan jika ingin menggukana versi 14 maka ketik "nvm use 14"

a

6. jika ingin mengecek versi ndan node maka ketik "npm -v" dan "node -v"

a

7. lalu buat file baru lalu ketik "npm init -y" untuk meng inisiasi file tersebut dan nanti akan tersintal file json.package

a

8. lalu ketik "npm install express --save" untuk menginstall framework dari node.js

a

9. Jika sudah buat file dengan nama index.js, dengan mengetik "nano index.js" dan isikan file tersebut dengan

const express = require("express");
const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("Hello World!");
});

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`);
});

a

10. untuk mejalankan node.js nya ketik "node index.js"

a




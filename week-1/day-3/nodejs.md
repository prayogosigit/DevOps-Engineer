# Langkah 1
1. Pertama-tama kita harus meng-install terlebih engine-nya dahulu. dengan cara "curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash"

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-3/assets/1.png)

2. jika NVM belum terdekteksi ketik "exec bash" untuk me refresh

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-3/assets/2.png)


4. Selanjutnya lakukan peng installan dengan keltik "nvm install 16" untuk nvm versi 16

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-3/assets/3.png)

5. untuk menggunakan nvm versin 16 ketik "nvm use 16" dan jika ingin menggukana versi 14 maka ketik "nvm use 14"

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-3/assets/4.png)

6. jika ingin mengecek versi ndan node maka ketik "npm -v" dan "node -v"

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-3/assets/5.png)

7. lalu buat file baru lalu ketik "npm init -y" untuk meng inisiasi file tersebut dan nanti akan tersintal file json.package

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-3/assets/6.png)

8. lalu ketik "npm install express --save" untuk menginstall framework dari node.js

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-3/assets/7.png)

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

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-3/assets/8.png)

10. untuk mejalankan node.js nya ketik "node index.js"

![logo](https://github.com/prayogosigit/DevOps-Engineer/blob/main/week-1/day-3/assets/9.png)




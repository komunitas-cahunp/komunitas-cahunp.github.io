---
layout: post

title: Upload File Menggunakan NodeJS
subtitle: "NodeJS dirancang untuk membangun aplikasi skala jaringan"
cover_image:

excerpt: "Pastikan mesin komputer anda sudah terinstall nodeJS, download dan install [nodeJS](https://nodejs.org), pembahasan ini akan membahas bagaimana *upload file* menggunakan [lien](https://github.com/LienJS/Lien) dan [formidable](https://github.com/felixge/node-formidable), setelah membuat server HTTP NodeJS."

author:
  name: M. Saiful Mukharom
  twitter: saifulindo
  bio: Teacher, Networking
  image: Gz7G7rNc.jpg
---

### Overview
Pastikan mesin komputer anda sudah terinstall nodeJS, download dan install [nodeJS](https://nodejs.org), pembahasan ini akan membahas bagaimana *upload file* menggunakan [lien](https://github.com/LienJS/Lien) dan [formidable](https://github.com/felixge/node-formidable), setelah membuat server HTTP NodeJS.

*line* adalah Framework mungil tingkat-tinggi yang digunakan untuk membuat server HTTP, sedangkan *formidable* adalah modul NodeJS untuk menguraikan data formulir dan upload file.

### Pembahasan
Pertama-tama, membuat struktur direktory:

```bash
# buat direktori proyek
$ mkdir file-upload

# masuklah kedalam direktori proyek
$ cd file-upload

# membuat direktori public dan uploads
$ mkdir -p public/uploads
```

Berikutnya anda harus meng-instal dependencies:

```bash
$ npm i fomidable@1.0.17 lien@0.0.8
```

Membuat file `index.html` kedalam direktori `public`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>File Upload</title>
</head>
<body>
  <form action="/upload" method="post" enctype="multipart/form-data">
    <input name="file" type="file">
    <button>Submit</button>
  </form>
  <iframe src="/upload/list" frameborder="0"></iframe>
</body>
</html>
```
Ini adalah halaman `HTML` yang berisi file bentuk formulir upload dan elemen `<iframe>` yang akan mendaftar file yang di upload (`uploads/list`).

Dan sekarang sisi server: `index.js`

```javascript
// Dependensies
var Lien = require("lien")
  , Fs = require("fs")
  , Formidable = require("formidable")
  ;

// Constans
const DIR_UPLOADS = __dirname + "/public/uploads/";

// Init lien Server
var server = new Lien({
    host: "localhost"
  , port: 9000

});

// Add Page
server.page.add("/", function (lien){
  lien.file("/index.html");
});

//Upload 
server.page.add("/upload$", function (lien){
  var form = new Formidable.IncomingForm(
    {uploadDir: DIR_UPLOADS}
    );
  form.parse(lien.req, function (err, fields, files){
    if (!files.file) {
      return lien.end("File is missing.", 400);
    }
    Fs.rename(files.file.path, DIR_UPLOADS + files.file.name, function (err){
      if (err) {
        return lien.end(err, 400);
      }
      lien.redirect("/");
    });
  });
});

// List
server.page.add("/upload/list", function (lien){
  Fs.readdir(DIR_UPLOADS, function  (err, files) {
    if (err) {return lien.end(err, 500);}
    files = files.filter(function(c){
      return c !== ".gitignore";
    });
    var list = ["<ul>", files.map(function(c){
      return["<li>", "<a target='blank' href='/uploads/", c, "'>", c, "</a></li>"].join("");
      }).join(""), "</ul>"].join("");
      lien.end(list);
  });
});
```

Dan begitu saja, server akan berjalan pada `localhost:9000`:

```bash
node index.js
```

Buka `localhost:9000` dan dimana anda bisa upload file dan melihat sebuah daftar upload sebelumnya:

<div class="full zoomable"><img src="/images/upload.png"></div>

### Sumber
- Bizău, Ionică,  2015. *Upload files using NodeJS*, (online). tersedia: http://ionicabizau.net/blog/22-upload-files-using-nodejs. diakses 06 Juni 2015.

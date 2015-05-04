---
layout: post

title: Version Control
subtitle: "Source Code Management"
cover_image:

excerpt: "Scott Scacon (2009:1) Penulis Buku ProGit mengatakan <i>Version control is a system that records changes to a file or set of files over time so that you can recall specific versions later</i>."

author:
  name: M. Saiful Mukharom
  twitter: saifulindo
  bio: Teacher, Networking
  image: Gz7G7rNc.jpg
---

Ada sekitar belasan sebuah aplikasi version control, diantaranya Bazar, BitKeeper,
Subversion, Git dan lainnya. Scott Scacon (2009:1) Penulis Buku ProGit mengatakan " *Version control is a system that records changes to a file or set of files over time so that you can recall specific versions later.*"
Yang pada kali ini saya akan membahas version control
Git, mulai dari :

### Setup dan Usage

Download Git dari sumbernya :

* [Windows](https://msysgit.github.com/)
* [Linux](https://www.kernel.org/pub/software/scm/git/)
* [Mac OS](http://git-scm.com/download/mac)

Untuk melihat tahapan - tahapan setup, bisa merujuk pada link berikut :
`https://github.com/komunitas-cahunp/installGit`

### Konfigurasi Awal
Untuk melakukan konfigurasi awal ikuti perintah berikut, konfigurasi awal ini di lakukan hanya sekali
untuk *global*-nya, sedangkan untuk konfigurasi per-`project` atau disebut dengan konfigurasi lokal ini sifatnya opsional
bisa di konfigurasi bisa tidak.

```
$ git config --global user.name "Nama Lengkap"
$ git config --global user.email "user@email.com"
```

### Perintah Dasar
Berikut ini beberapa perintah dasar yang perlu diketahui ketika mengoperasikan Git Bash.

* Perintah Operasi file dan direktory

```
$ touch
$ cp
$ rm
$ mv
$ mkdir
$ rm -rf
$ cd
$ ls
```

* Perintah *Local Repository*

```
$ git init
$ git add
$ git commit
$ git remote
```

* Perintah Kolaborasi

```
$ git clone
$ git pull
$ git push
$ git fetch
```
Penjelasan lebih lanjut mengenai perintah diatas bisa merujuk pada link berikut :
` https://www.gitbook.com/book/saifulindo/contekan-git/details`.

### Bekerja dengan `GitHub.com`
* Daftar Akun [GitHub.com](https://github.com/)
* Bekerja menggunakan protokol *SSH*, untuk mengijinkan anda melakukan `clone`, `pull`, `Fetch`, dan `Push` menggunkan *URLs SSH.*
  - Generating *SSH-Keygen*

    ```
    $ ssh-keygen -t rsa -C "alamat_email"
    $ ls ~/.ssh/
    ```
  - Kopi `id_rsa.pub`

    ```
    $ clip < ~/.ssh/id_rsa.pub
    ```
  - Tambahkan `public_key` ke akun GitHub.com
    <div class="full zoomable"><img src="/images/ssh-key.png"></div>
    Sumber Gambar-vc1: (Włodzimierz Gajda: 329)
  - Buat *Repository* Baru
    <div class="full zoomable"><img src="/images/new-repo.png"></div>
    Sumber Gambar-vc2 : (Włodzimierz Gajda: 331)
  - Kopi proyek yang sudah ada atau buat file baru contoh : `README.md`
    <div class="full zoomable"><img src="/images/new-repo-col.png"></div>
    Sumber Gambar-vc3 : (Włodzimierz Gajda: 332)<br \>
    Jika anda memutuskan untuk membuat file baru maka, anda lakukan perintah:

    ```
    $ mkdir 12-03
    $ cd 12-03/
    $ touch README.md
    $ git add README.md
    $ git commit -m "Pesan Perubahan"
    $ git remote add origin git@github.com:<username>/12-03.git
    $ git push -u origin master
    ```
    Jika anda memutuskan untuk mengkopi proyek yang sudah ada maka lakukan perintah:

    ```
    $ git add --all
    $ git commit -m "Pesan Perubahan"
    $ git remote add origin git@github.com:<username>/12-03.git
    $ git push -u origin master
    ```
    Oke Selesai, Semoga bermanfaat, jika ada pertanyaan buatlah diskusi dan persoalan di alamat :
    `https://github.com/komunitas-cahunp/komunitas-cahunp.github.io/issues` dengan judul: **Post Version Control #Subtitle-issue**, contoh :`Post Version Control #Perintah git pull`.

### Sumber
- Włodzimierz, Gajda, 2013. *Git Recipes - A Problem-Solution Approach*, Poland:Apress.
- Scott, Chacon, 2009. *Pro Git*, https://github.s3.amazonaws.com/media/progit.en.pdf, Visited 01/05/2015.

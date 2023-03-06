# Package Mangement

## Evolusi Sistem Operasi

<div style="text-align: right"> Sistem operasi adalah program yang bertindak sebagai perantara antara pengguna komputer dan perangkat keras komputer. Tujuan dari sistem operasi adalah untuk menyediakan lingkungan di mana pengguna dapat menjalankan program. Tujuan utamanya adalah untuk membuat sistem komputer nyaman digunakan. Tujuan kedua adalah menggunakan perangkat keras komputer dengan cara yang efisien. Sistem komputer secara kasar dapat dibagi menjadi empat komponen: perangkat keras, sistem operasi, program aplikasi, dan pengguna. Perangkat keras – unit pemrosesan pusat (CPU), memori, dan perangkat input/output (I/O) – menyediakan sumber daya komputasi dasar. Program aplikasi - seperti kompiler, sistem basis data, permainan, dan program bisnis - menentukan cara sumber daya ini digunakan untuk memecahkan masalah komputasi pengguna. Mungkin ada banyak pengguna yang berbeda dan banyak program aplikasi yang berbeda. Sistem operasi mengontrol dan mengoordinasikan penggunaan perangkat keras di antara berbagai program aplikasi untuk berbagai pengguna. </div>


## Perbedaan antara perintah sudo dan su pada Linux
Menjadi root dengan SU berarti sedang berada di -root, yang berarti sama dengan masuk ke terminal sebagai pengguna root dengan kata sandi Root. Dan itu berbahaya karena berbagai alasan.
Ketika masuk sebagai root maka ada akses untuk:
- Hapus  semua file
- Ubah izin semua file
- Mengubah akun user
- Menginstall atau membuka sistem file
- Mengapus atau install software
- Membuat, mengahapus, dan mengubah file system

Pada dasarnya, sebagai root user dapat melakukan apa saja yang ada pada sistem. Maka jika terjadi kesalahan yang dibuat sebagai user root dapat menghancurkan sistem. Alternatifnya adalah dengan menggunakan sudo.

## Sudo
Sudo merupakan akronim dari superuser do atau pengganti user, yaitu perintah yang menjalankan prompt root tanpa harus mengubah identitas pengguna. Untuk menggunakan perintah root pada pengguna lain maka bisa diubah pada konfigurasi yang ada di file /etc/sudoers. Untuk bisa menjalanakan perintah yang ada di root, maka harus menggunakan perintah sudo. Contoh, jika ingin menginstall package nginx, apabila menggunakan perintah:
```sh
dnf install nginx
```
Jika menggunakan perintah diatas maka akan error karena tidak sebagai root atau di grup sudo. Maka alternatifnya dapat menjalankan perintah berikut:
```sh
sudo dnf install nginx
```
Namun apabila menggunakan perintah tersebut maka akan diminta untuk mengetikkan password terlebih dahulu baru bisa menjalankan perintah dengan catatan apabila user tersebut adalah bagian dari grup sudo. Namun ada cara lain agar dapat menjalankan beberapa perintah yang ada di sbin, dengan menggunakan user lain tanpa harus mengetikkan password terlebih dahulu , yaitu sebagai berikut
1. Masuk sebagai su -
```sh
su -
```
2. Ketikkan perintah visudo
```sh
visudo
```
3. Lalu akan membuka file yang ada pada direktori /etc/sudores.tmp, lalu pada bagian User  privilege specification tambahkan user anda. Contoh disini nama user saya adalah nabila maka tambahkan seperti berikut:
```sh
nabila ALL=(ALL:ALL) ALL
```
seperti pada gambar dibawah ini

![Langkah 2](https://github.com/hanifnabila/Package-Management/blob/main/img/2.png)

4. Jika sudah ditambahkan, simpan dan keluar dengan menekan tombol ctrl+x, lalu enter.
5. Buka file direktori /etc/group dengan mengetikkan perintah
```sh
nano /etc/group
```
   Pada baris pertama yaitu dibagian `root:x:x:0:`, tambahkan nama user yang ingin diberikan akses.
   ![Langkah 2](https://github.com/hanifnabila/Package-Management/blob/main/img/3.png)
      
## Su

Su adalah akronim untuk switch user atau substitute user. Pada dasarnya perintah ini beralih ke pengguna tertentu dan memerlukan kata sandi untuk pengguna yang diganti. Yang sering digunakan adalah beralih ke akun root tetapi bisa juga beralih ke akun apapun yang ada di sistem.
Sebagai contoh, jika mengetikkan:
```sh
$ su -
```
Pada contoh diatas maka akan beralih ke root dan membutuhkan password root. Dengan menambahkan (-) berarti memberikan layanan root environment (variabel path dan shell) sehingga dengan mudah memberikan root user power menggunakan single command dan tetap menjaga environment user.
```sh
$ su nabila
```
Pada contoh kedua, ini hanya beralih ke nabila. Dan membutuhkan password dari user nabila. Jika ingin beralih ke akun nabila termasuk juga path dan environment, maka tambahkan opsi (-).
```sh
$ su - nabila
```
Opsi - memiliki efek yang sama dengan masuk ke sistem secara langsung dengan akun pengguna tersebut. Intihnya, akan menjadi pengguna tersebut.
```sh
$ su
```
Apabila hanya mengetikkan perintah su saja tanpa tanda (-) berarti masuk ke direktori /bin sehingga tidak masuk ke environment root. Dan membutuhkan password root.

Package Management

# APT
Perintah Apt adalah command-line tool, yang bekerja dengan APT ubuntu berfungsi seperti melakukan installasi package software, update package software yang ada, update index daftar package, dan bahkan upgrade sistem ubuntu.

## Setting Repository

1. Tambahkan Paket Repo
Buka file `/etc/apt/sources.list` menggunakan editor nano dan tambahkan repository source di bawah ini. Kemudian save dan close dengan menggunakan Ctrl+X.
```sh
deb http://deb.debian.org/debian bullseye main
deb-src http://deb.debian.org/debian bullseye main
```
Tampilannya akan seperti gambar di bawah ini

![Langkah 2](https://github.com/hanifnabila/Package-Management/blob/main/img/4.png)

2. Update Server 
Langkah selanjutnya yaitu update package menggunakan command `apt update` or `apt-get update` seperti gambar berikut ini

![Langkah 2](https://github.com/hanifnabila/Package-Management/blob/main/img/5.png)

## Install Package
Setelah konfigurasi repository, sekarang sudah bisa menginstall sebuah package menggunakan perintah `apt-get install`

- Install package mc
```sh
apt-get install mc
```
![Langkah 2](https://github.com/hanifnabila/Package-Management/blob/main/img/6.png)

- Install package net-tools
```sh
apt-get install net-tools
```
![Langkah 2](https://github.com/hanifnabila/Package-Management/blob/main/img/7.png)

- Install package htop
```sh
apt-get install htop
```
![Langkah 2](https://github.com/hanifnabila/Package-Management/blob/main/img/8.png)

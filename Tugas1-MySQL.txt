// masuk kedalam mariadb dengan xampp
C:\Users\acer>cd \xampp\mysql\bin
C:\xampp\mysql\bin>mysql -u root -p

// untuk melihat 
MariaDB [(none)]> show databases;

//membuat database baru
MariaDB [(none)]> CREATE DATABASE dbtoko;

// masuk database
MariaDB [(none)]> USE dbtoko;

// membuat table katu
MariaDB [dbtoko]> CREATE TABLE kartu(
    -> id int NOT NULL auto_increment primary key,
    -> kode varchar(10) unique,
    -> nama varchar(30) NOT NULL,
    -> diskon double default 0,
    -> iuran double default 0);

// membuat table pelanggan
CREATE TABLE pelanggan(
    -> id int NOT NULL auto_increment primary key,
    -> kode varchar(10) unique,
    -> nama varchar(45),
    -> jk char(1),
    -> tmp_lahir varchar(30),
    -> tgl_lahir date,
    -> email varchar(45),
    -> kartu_id int NOT NULL references kartu(id));

// membuat table pesanan
CREATE TABLE pesanan(
    -> id int NOT NULL auto_increment primary key,
    -> tanggal date,
    -> total double,
    -> pelanggan_id int NOT NULL REFERENCES pelanggan(id));

// membuat table pembayaran
CREATE TABLE pembayaran(
    -> id int NOT NULL auto_increment primary key,
    -> no_kuitansi varchar(10) unique,
    -> tanggal date,
    -> jumlah double,
    -> ke int,
    -> pesanan_id int NOT NULL REFERENCES pesanan(id));

// membuat table jenis produk
CREATE TABLE jenis_produk(
    -> id int NOT NULL auto_increment primary key,
    -> nama varchar(45));

ALTER TABLE jenis_produk
    -> ADD COLUMN keterangan varchar(30) AFTER nama;

 ALTER TABLE jenis_produk
    -> CHANGE keterangan ket varchar(30);

ALTER TABLE jenis_produk
    -> MODIFY ket varchar(50) AFTER nama;


// TUGAS 1 MySQL
// membuat table produk
CREATE TABLE produk(
    -> id int NOT NULL auto_increment primary key,
    -> kode varchar(10) unique,
    -> nama varchar(45),
    -> harga_beli double,
    -> harga_jual double,
    -> stok int,
    -> min_stok int,
    -> jenis_produk_id int NOT NULL REFERENCES jenis_produk(id));

// membuat table pesanan items
CREATE TABLE pesanan_items(
    -> id int NOT NULL auto_increment primary key,
    -> produk_id int NOT NULL REFERENCES produk(id),
    -> pesanan_id int NOT NULL REFERENCES pesanan(id),
    -> qty int,
    -> harga double);

// membuat table vendor
CREATE TABLE vendor(
    -> id int NOT NULL auto_increment primary key,
    -> nomor varchar(4),
    -> nama varchar(40),
    -> kota varchar(30),
    -> kontak varchar(30));

// membuat table pembelian
CREATE TABLE pembelian(
    -> id int NOT NULL auto_increment primary key,
    -> tanggal varchar(45),
    -> nomor varchar(10),
    -> produk_id int NOT NULL REFERENCES produk(id),
    -> jumlah int,
    -> harga double,
    -> vendor_id int NOT NULL REFERENCES vendor(id));

// menambahkan alamat pada pelanggan dengan tipe data varchar (40)
ALTER TABLE pelanggan
    -> ADD COLUMN alamat varchar(40) AFTER tgl_lahir;

// mengubah kolom nama pada pelanggan menjadi nama_pelanggan
 ALTER TABLE pelanggan
    -> CHANGE nama nama_pelanggan varchar(45);

// edit tipe data nama_pelanggan menjadi varchar(50)
 ALTER TABLE pelanggan
    -> MODIFY nama_pelanggan varchar(50) AFTER kode;

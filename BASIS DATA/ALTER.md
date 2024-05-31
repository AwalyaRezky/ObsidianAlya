Berikut Struktur Awal

# Menambahkan Kolom
## Struktur Query
```mysql
ALTER TABLE (nama_tabel) ADD (nama_kolom_baru) (tipe_data) (`opsional` = AFTER (nama_kolom));
```
## Contoh Query
```mysql
ALTER TABLE mobil ADD batas_peminjaman varchar(10) AFTER peminjaman;
```
## Hasil
BEFORE
![gambar](ASET/alter1.png)
AFTER
![gambar](ASET/alter2.png)

## Analisis
- `ALTER TABLE`: Ini adalah perintah SQL yang digunakan untuk memodifikasi struktur tabel yang ada.
- `mobil`: merupakan nama tabel yang diubah.
- `ADD`: Kata kunci ini menunjukkan bahwa sebuah kolom baru ditambahkan ke dalam tabel.
- `batas_peminjaman`: Ini adalah nama kolom baru yang ditambahkan.
- `varchar(10)`: Ini menentukan tipe data dari kolom baru. `varchar` adalah string karakter berpanjang variabel, dan `(10)` menunjukkan bahwa itu dapat menampung hingga 10 karakter.
- `AFTER peminjaman`: Ini menentukan posisi di mana kolom baru akan ditambahkan. Dalam hal ini, itu akan ditambahkan setelah kolom `peminjaman`.
## Kesimpulan
Jadi, kesimpulan program ini adalah bahwa ia menambahkan kolom `batas_peminjaman` ke tabel `mobil`, di mana kolom baru tersebut merupakan `string` teks dengan panjang maksimal 10 karakter, dan kolom ini akan ditempatkan setelah kolom `peminjaman` dalam struktur tabel.
## Tambahan
### Query
```mysql
 UPDATE mobil SET batas_peminjaman='2024-04-24' WHERE peminjaman IS NOT NULL;
```
### Hasil
![gambar](ASET/alter3.png)

# Mengubah Nama Kolom
## Struktur Query
```mysql
ALTER TABLE (nama_tabel) CHANGE (nama_kolom_yg_dignti) (nama_kolom_baru) (tipedata);
```
## Contoh Query
```mysql
ALTER TABLE mobil CHANGE batas_peminjaman deadline varchar(10);
```
## Hasil
![gambar](ASET/rename.png)

## Analisis
- `ALTER TABLE`: Ini adalah perintah SQL yang digunakan untuk memodifikasi struktur tabel yang sudah ada.
- `mobil`: Ini adalah nama tabel yang akan diubah.
- `CHANGE batas_peminjaman deadline varchar(10)`: Ini adalah perintah untuk mengubah nama dan tipe data kolom. Kolom yang sebelumnya bernama `batas_peminjaman` akan diubah menjadi `deadline`. Selain itu, tipe data kolom ini diubah menjadi `varchar(10)`, yang berarti itu adalah string teks dengan panjang maksimal 10 karakter.

## Kesimpulan
Kesimpulan perintah ini melakukan dua perubahan pada tabel `mobil`: mengubah nama kolom dari `batas_peminjaman` menjadi `deadline`, dan mengubah tipe data kolom tersebut menjadi `varchar(10)`.

# Mengubah Tipe Data Kolom
## Struktur Query
```MYSQL
ALTER TABLE (nama_tabel) MODIFY (nama_kolom) (nama_tipedata);
```
## Contoh Query
```MYSQL
ALTER TABLE mobil MODIFY deadline DATE;
```
## Hasil
![gambar](ASET/modify.png)

## Analisis
- `ALTER TABLE` adalah perintah SQL yang digunakan untuk mengubah struktur tabel yang sudah ada.
- `mobil` adalah nama tabel yang akan diubah.
- `MODIFY deadline DATE` adalah klausa yang menentukan kolom `deadline` yang akan diubah dan tipe datanya menjadi `DATE`.
## Kesimpulan
Kesimpulannya, program `ALTER TABLE mobil MODIFY deadline DATE;` digunakan untuk mengubah tipe data kolom `deadline` dalam tabel `mobil` menjadi `DATE`. Perubahan ini memungkinkan kolom `deadline` untuk hanya menyimpan nilai tanggal, dan memungkinkan operasi dan pemrosesan yang lebih tepat terhadap data tanggal yang terkait.
# Menambahkan constraint
## Struktur Query
```MYSQL
ALTER TABLE (nama_tabel)
    -> ALTER (nama_kolom) SET DEFAULT (nilai_default );
```
## Contoh Query
```MYSQL
ALTER TABLE mobil
    -> ALTER deadline SET DEFAULT 'Ready';
```
## Hasil
![gambar](ASET/ready.png)

## Analisis
- `ALTER TABLE`adalah SQL
- `mobil`adalah sebuah nama tabel
- `ALTER deadline`adalah sebuah klausa`deadline`dalam`desc_mobil`
- `SET DEFAULT 'Ready'`adalah`deadline`kolom
## Kesimpulan
Program `ALTER TABLE mobil ALTER deadline SET DEFAULT 'Ready';` mengubah nilai default kolom `deadline` dalam tabel `mobil` menjadi `'Ready'`. Ini berarti bahwa jika tidak ada nilai yang diberikan secara eksplisit saat melakukan operasi `INSERT` pada tabel `mobil`, maka kolom `deadline` akan memiliki nilai default `'Ready'`.
## Tambahan
### Query
```mysql
INSERT INTO mobil
    -> (id_mobil,no_plat,no_mesin,warna,pemilik,peminjaman,harga_rental)
    -> VALUES (7,"DD 4637 AL","ABC6547","MERAH","ALYA",NULL,200000);
```
### Hasil
![gambar](ASET/insert.png)

## Referensi tambahan
https://revou.co/panduan-teknis/sql-constraint
# Menghapus constraint
## Struktur Query
```MYSQL
 ALTER TABLE (nama_tabel)
    -> ALTER (nama_kolom) DROP DEFAULT;
```
## Contoh Query
```MYSQL
 ALTER TABLE mobil
    -> ALTER deadline DROP DEFAULT;
```
## Hasil
![gambar](ASET/dropconstrain.png)

## Analisis
- `ALTER TABLE` adalah perintah SQL yang digunakan untuk mengubah struktur tabel yang sudah ada.
- `mobil` adalah nama tabel yang akan diubah.
- `ALTER deadline` adalah klausa yang menentukan kolom `deadline` yang akan diubah.
- `DROP DEFAULT` adalah klausa yang digunakan untuk menghapus nilai default dari kolom.
## Kesimpulan
Program `ALTER TABLE mobil ALTER deadline DROP DEFAULT;` menghapus nilai default dari kolom `deadline` dalam tabel `mobil`. Setelah menjalankan program ini, kolom `deadline` tidak akan memiliki nilai default, dan jika tidak ada nilai yang diberikan secara eksplisit saat melakukan operasi `INSERT`, kolom `deadline` akan memiliki nilai `NULL`.
## Referensi tambahan
https://www.geeksforgeeks.org/sql-drop-constraint
# Menghapus kolom
## Struktur Query
```mysql
ALTER TABLE mobil DROP COLUMN deadline;
```
## Contoh Query
```mysql
ALTER TABLE mobil DROP COLUMN deadline;
```
## Hasil
![gambar](ASET/drop(2).PNG)

## Analisis
- `ALTER TABLE`adalah perintah SQL yang digunakan untuk mengubah struktur tabel yang ada.
- `mobil`adalah nama tabel yang sedang diubah.
- `DROP COLUMN`adalah klausa yang digunakan untuk menghapus kolom tertentu dari tabel.
- `deadline`adalah nama kolom yang dihilangkan dari `mobil`tabel.
## Kesimpulan
Singkatnya, program ini menginstruksikan sistem manajemen basis data untuk menghapus `deadline`kolom dari `mobil`tabel. Setelah menjalankan program ini, `deadline` kolom tersebut tidak akan ada lagi di struktur tabel, dan data apa pun yang disimpan di kolom tersebut akan dihapus secara permanen.
# Mengganti nama tabel
## Struktur Query
```mysql
 ALTER TABLE mobil RENAME TO daftar_mobil;
```
## Contoh Query
```mysql
 ALTER TABLE mobil RENAME TO daftar_mobil;
```
## Hasil
![gambar](ASET/rename(2).png)

## Analisis
- `ALTER TABLE` adalah perintah SQL yang digunakan untuk mengubah struktur tabel yang sudah ada.
- `mobil` adalah nama tabel yang akan diubah.
- `RENAME TO` adalah klausa yang digunakan untuk mengubah nama tabel.
- `daftar_mobil` adalah nama baru yang diberikan kepada tabel.
## Kesimpulan
Program `ALTER TABLE mobil RENAME TO daftar_mobil;` mengubah nama tabel `mobil` menjadi `daftar_mobil`. Setelah menjalankan program ini, tabel yang sebelumnya bernama `mobil` akan berganti nama menjadi `daftar_mobil`.

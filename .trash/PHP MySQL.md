# Koneksi Database

## penjelasan
Koneksi database adalah proses menghubungkan aplikasi atau sistem perangkat lunak dengan database agar bisa melakukan operasi seperti penyimpanan, pengambilan, pembaruan, dan penghapusan data.
 
 ## program
 ```php
 <?php

$koneksi = mysqli_connect('localhost', 'root', '', 'rental_fina');
  
if ($koneksi) {

    echo "<br> koneksi aman <br>";

} else {

    echo "error, tidak bisa koneksi ke database";

}

//jalankan query selesai

$select = mysqli_query($koneksi, "SELECT * FROM mobil");

//membuat

$result =mysqli_fetch_assoc($select);

//var_dumb($result);

echo 'Berikut mobil-mobil beserta pemiliknya<br>';


$a = 1;

foreach ($select as $key => $data) {

    echo $a++ . ". " . $data['no_plat'] . " : " . $data['pemilik'] . '<br>';

}

//echo '<p>Halo ' . $result['pemilik'] . '!!</p><br>';
```
 
## hasil

 ![gambar](ASET/php1.png)
 
## analisis
 - Koneksi ke database: Kode menggunakan fungsi `mysqli_connect` untuk menghubungkan ke database `rental_fina` yang berada di localhost dengan username `root` dan password kosong. Jika koneksi berhasil, maka akan menampilkan pesan "koneksi aman".
- Eksekusi query: Kode menggunakan fungsi `mysqli_query` untuk menjalankan query SQL `SELECT * FROM mobil` yang digunakan untuk mengambil semua data dari tabel `mobil`.
- Mengambil hasil query: Kode menggunakan fungsi `mysqli_fetch_assoc` untuk mengambil hasil query dan menyimpannya dalam variabel `$result`. Fungsi ini mengembalikan array yang berisi hasil query dalam bentuk associative array.
- Menampilkan data: Kode menggunakan loop `foreach` untuk menampilkan data mobil beserta pemiliknya. Namun, ada kesalahan pada kode ini. Kode menggunakan variabel `$select` yang berisi hasil query, tetapi tidak dapat di-looping menggunakan `foreach` karena `$select` adalah resource, bukan array. Seharusnya menggunakan `$result` yang berisi hasil query dalam bentuk array.
# Tampilan Data
## penjelasan
Tampilan data adalah proses menampilkan data yang telah disimpan dalam database ke antarmuka pengguna, baik itu di aplikasi desktop, web, atau mobile. Tujuan dari tampilan data adalah untuk menyediakan cara yang mudah dan efisien bagi pengguna untuk melihat, memahami, dan berinteraksi dengan data.
## program
```php
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>index tabel</title>

</head>

<body>

    <h2>Data Siswa Berprestasi</h2>

    <a href="tambah.php">+Tambah Data Baru</a><br><br>

    <p>

        <a href="export.php">Export ke Excel</a>

    </p>

    <table border="5">

    <tr>

        <th>id_siswa</th>

        <th>Gambar</th>

        <th>nama</th>

        <th>email</th>

        <th>jenis_kelamin</th>

        <th>alamat</th>

        <th>Aksi</th>

    </tr>

  

    <?php

    include "koneksi.php";

    $i = 1;

    $query = mysqli_query($koneksi, "SELECT * FROM siswa");

    while ($data = mysqli_fetch_array($query)) {

    ?>

  

    <tr>

        <td><?php echo $i; ?></td>

        <td>

            <img src="img/<?= $data['gambar'] ?>" alt="gambar" width="100px">

        </td>

        <td><?php echo $data['nama']; ?></td>

        <td><?php echo $data['email']; ?></td>

        <td><?php echo $data['jenis_kelamin']; ?></td>

        <td><?php echo $data['alamat']; ?></td>

  

        <td>

            <a href="ubah.php?id=<?= $data['id_siswa']; ?>">Ubah</a> |

            <a href="hapus.php?id=<?= $data['id_siswa']; ?>">Hapus</a> |

        </td>

    </tr>

    <?php

    $i++;

    }

    ?>

    </table>

</body>

</html>
```
## hasil
![gambar](ASET/php2.png)

## analisis
# Tambahkan Data
## penjelasan
## program
```php
<!DOCTYPE html>

<html lang="en">

  

<head>

    <title>Document</title>

</head>

  

<body>

    <h2>Tambah Data</h2>

    <?php

    include "koneksi.php";

  

    function upload(): string

{

  

    $nameImage = $_FILES['gambar']['name'];

    $directoryFile = $_FILES['gambar']['tmp_name'];

    $errorImage = intval($_FILES['gambar']['error']);

    $sizeFile = $_FILES['gambar']['size'];

  

    // cek apakah gambar ada

    if ($errorImage === 4) {

        echo "<script>alert('Anda Belum Upload Gambar')</script>";

        return false;

    }

  

    // mengambil ekstensi file

    $validType = ['svg', 'jpg', 'png', 'jpeg', 'webp'];

    $extensionFile = explode(".", $nameImage);

    $extensionValid = strtolower(end($extensionFile));

  

    // cek apakah yang diupload gambar atau bukan

    if (!in_array($extensionValid, $validType)) {

        echo "<script>alert('yang anda Upload bukan gambar')</script>";

        return false;

    }

  

    // cek size file

    if ($sizeFile > 3_000_000) {

        echo "<script>alert('Ukuran File Terlalu Besar!!(Maks 3MB)')</script>";

        return false;

    }

  

    // upload file

    $nameImage = uniqid() . "." . $extensionValid;

    move_uploaded_file($directoryFile, "img/{$nameImage}");

  

    // mengembalikan namafile yg sudah divalidasi

    return $nameImage;

}

  
  

    if (isset($_POST['simpan'])) {

        $nama = $_POST['nama'];

        $email = $_POST['email'];

        $jenis_kelamin = $_POST['jenis_kelamin'];

        $alamat = $_POST['alamat'];

  

        $gambar = upload();

        if (!$gambar) {

            return false;

        }

  

        // * true / false

        $query = mysqli_query($koneksi, "INSERT into siswa(nama,email,jenis_kelamin,alamat,gambar)

        values ('$nama','$email','$jenis_kelamin','$alamat','$gambar')");

  

        if ($query == true) {

            echo "<script>

            alert('Tambah data Berhasil')

            window.location.href='table.php'

            </script>";

        } else {

            echo '<script>alert("Tambah data gagal")</script>';

        }

    }

  
  

    ?>

    <form method="post" enctype="multipart/form-data">

        <table>

            <tr>

                <td>Nama</td>

                <td><input type="text" name="nama"></td>

            </tr>

            <tr>

                <td>Email</td>

                <td><input type="text" name="email"></td>

            </tr>

            <tr>

                <td>Jenis Kelamin</td>

                <td>>

                    <select name="jenis_kelamin">

                        <option>Laki-laki</option>

                        <option>Perempuan</option>

                    </select>

                </td>

            </tr>

  

            <tr>

                <td>Alamat</td>

                <td><input type="text" name="alamat"></td>

            </tr>

  

            <tr>

                <td>Gambar</td>

                <td><input type="file" name="gambar"></td>

            </tr>

  

            <tr>

                <td></td>

                <td>

                    <button name="simpan" type="submit">Simpan</button>

                    <button type="reset">Reset</button>

                    <a href="table.php">Kembali</a>

                </td>

            </tr>

        </table>

    </form>

  

</body>

  

</html>
```
## hasil
![gambar](ASET/php3.png)

![gambar](ASET/php4.png)

## analisis
# Ubah Data
## penjelasan
## program
```php
<!DOCTYPE html>

<html lang="en">

  

<head>

    <title>Document</title>

</head>

  

<body>

    <h2>Ubah Data</h2>

    <?php

    include "koneksi.php";

  

    $id = $_GET['id'];

  

    if (isset($_POST['simpan'])) {

        $nama = $_POST['nama'];

        $email = $_POST['email'];

        $jenis_kelamin = $_POST['jenis_kelamin'];

        $alamat = $_POST['alamat'];

  

        $query = mysqli_query($koneksi, "UPDATE siswa SET

                                        nama='$nama',

                                        email='$email',

                                        jenis_kelamin='$jenis_kelamin',

                                        alamat='$alamat'

                                        WHERE id_siswa=$id");

        if ($query) {

            echo "<script>

            alert('ubah data Berhasil')

            window.location.href='table.php'

            </script>";

        } else {

            echo '<script>alert("ubah data gagal")</script>';

        }

    }

  

    $query = mysqli_query($koneksi, "SELECT * FROM siswa where id_siswa=$id");

    $data = mysqli_fetch_array($query);

    if ($data == "") {

        die('Data tidak ada');

    }

    ?>

  

    <form method="post">

        <table>

            <tr>

                <td>Nama</td>

                <td><input type="text" value="<?= $data['nama'] ?>" name="nama"></td>

            </tr>

            <tr>

                <td>Email</td>

                <td><input type="text" value="<?= $data['email'] ?>" name="email"></td>

            </tr>

            <tr>

                <td>Jenis Kelamin</td>

                <td>>

                    <select name="jenis_kelamin">

                        <option <?php if ($data['jenis_kelamin'] == "laki-laki")

                            echo 'selected'; ?>>Laki-laki</option>

                        <option <?php if ($data['jenis_kelamin'] == "perempuan")

                            echo 'selected'; ?>>Perempuan</option>

                    </select>

                </td>

            </tr>

  

            <tr>

                <td>Alamat</td>

                <td><input type="text" value="<?= $data['alamat'] ?>" name="alamat"></td>

            </tr>

  

            <tr>

                <td></td>

                <td>

                    <button name="simpan" type="submit">Ubah</button>

                    <button type="reset">Reset</button>

                    <a href="table.php">Kembali</a>

                </td>

            </tr>

        </table>

    </form>

  

</body>

  

</html>
```
## hasil
![gambar](ASET/php5.png)

![gambar](ASET/php6.png)

## analisis
# Hapus Data
## penjelasan
## program
```php
<?php

  

include('koneksi.php');

  

if(isset($_GET['id'])){

  
  

    $id = $_GET['id'];

  

    $query = mysqli_query($koneksi, "DELETE FROM siswa WHERE id_siswa = $id");

  

   if($query) {

            echo "<script>

            alert('Hapus data Berhasil')

            window.location.href='table.php'

            </script>";

        }else {

            echo '<script>alert("Hapus data gagal")</script>';

        }

}

  

?>
```
## hasil
![gambar](ASET/php7.png)

## analisis
# Session/Login
## session
### penjelasan
Session adalah periode interaksi antara pengguna dan aplikasi web, di mana data tertentu disimpan di server untuk melacak informasi pengguna saat mereka menavigasi dari satu halaman ke halaman lain. Data yang disimpan dalam session biasanya berisi informasi penting seperti identitas pengguna, preferensi, status login, dan data lainnya yang perlu dipertahankan selama kunjungan pengguna.
### program
```php
<?php

session_start();

// $username = "fatir";
// $alamat = "muh jufri 4";
  
// $_SESSION['username'] = $username;
// $_SESSION['alamat'] = $alamat;

if (isset($_POST['submit'])){
    $username = $_POST['username'];
    $password = $_POST['password'];

$koneksi = mysqli_connect('localhost', 'root', '', 'mada') or die('error koneksi');
    $result = mysqli_query($koneksi, "SELECT * FROM user WHERE username = '$username' AND password = '$password'");

    $data = mysqli_fetch_assoc($result);

    if(isset($data)) {
        $_SESSION['username'] = $data['username'];
        $_SESSION['nama'] = $data['nama'];
        $_SESSION['status'] = 'login';
        header('Location: user.php');
    } else {
        echo "username dan password salah";
    }
    var_dump($data);
}
?>

<!DOCTYPE HTML>
<html>
    <head>
       <title>login session</title>      
    </head>
    <body>
        <form method="post">
            <label >username</label>
            <input type="text" name="username">
            <br>
            <label >Password</label>
            <input type="password" name="password">
            <br>
            <button type="submit" name="submit">Login</button>
        </form>
    </body>
</html>
```
### hasil
![gambar](php8.png)
### analisis
- Kode dimulai dengan memeriksa apakah `submit`tombol di formulir telah diklik. Ini digunakan `isset($_POST['submit'])`untuk tujuan ini.
- Jika formulir dikirimkan, kode akan mengekstrak nilai nama pengguna dan kata sandi dari formulir menggunakan `$_POST['username']`dan `$_POST['password']`, masing-masing.
 - Ini membuat koneksi ke database MySQL yang diberi nama `mada`menggunakan `mysqli_connect`kredensial ( `localhost`, , (kata sandi kosong), dan ). `root` `''``mada`
 - Jika koneksi gagal, pesan kesalahan akan ditampilkan ( `error koneksi`).
- Ini membuat kueri SQL untuk memilih semua kolom ( `*`) dari `user`tabel tempat `username`dan `password`cocok dengan nilai yang diberikan. Kueri ini rentan terhadap serangan injeksi SQL (dijelaskan nanti).
- Kueri dijalankan menggunakan `mysqli_query`.
- Hasilnya diambil sebagai array asosiatif menggunakan `mysqli_fetch_assoc`.
- Ia memeriksa apakah `isset($data)`ada `true`. Hal ini menunjukkan jika catatan pengguna ditemukan dengan kredensial yang cocok.
- Jika ditemukan record ( `isset($data)`is `true`), berarti login berhasil.
- Kode (kemungkinan) memulai sesi PHP menggunakan `session_start()`jika belum dimulai. Sesi digunakan untuk menyimpan informasi spesifik pengguna di seluruh permintaan halaman.
- Ini menetapkan beberapa variabel sesi untuk menyimpan nama pengguna, nama (dengan asumsi `nama`ada dalam tabel), dan `login`indikator status.
- Header `Location`dikirim `header('Location: user.php')`untuk mengarahkan pengguna ke halaman bernama `user.php`, yang bisa berupa halaman dasbor atau profil.
- Jika login gagal ( `isset($data)`is `false`), maka akan muncul pesan error dalam bahasa Indonesia yang menunjukkan username dan password salah.
- Pernyataan tersebut `var_dump($data)`(mungkin untuk tujuan pengembangan) mencetak isi array `$data`, yang akan berisi informasi pengguna jika login berhasil. Ini dapat berguna untuk men-debug masalah login.
## user
### penjelasan
User PHP mengacu pada pengguna (user) dalam konteks aplikasi atau sistem yang dibangun menggunakan bahasa pemrograman PHP. Dalam aplikasi web berbasis PHP, pengguna biasanya dikelola melalui berbagai cara, termasuk otentikasi, otorisasi, dan manajemen sesi.
### program
```php
<?php

session_start();

if ($_SESSION['status'] == 'login' && $_SESSION['username'] == 'admin') {
    header("Location: admin.php");
}
if ($_SESSION['status'] != 'login') {
    header('Location: session.php');
}
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
</head>
<body>
    <h1>Halaman User</h1>
    <h1>Halo, <?= $_SESSION['nama'] ?></h1>
    <a href="logout.php">Logout</a>
</body>
</html>
```
### hasil
![gambar](ASET/php9.png)
### analisis
 - Kode memulai sesi PHP menggunakan `session_start()`. Ini penting untuk mengakses dan memanipulasi variabel sesi di seluruh skrip.
- Ia melakukan pemeriksaan bersyarat untuk melihat apakah dua variabel sesi, dan , ada dan memiliki nilai tertentu: `status``username`
- `$_SESSION['status'] == 'login'`: Ini memverifikasi apakah status login pengguna diatur ke "login".
- `$_SESSION['username'] == 'admin'`: Ini mengonfirmasi jika nama pengguna yang disimpan dalam sesi tersebut adalah "admin".
- Jika kedua kondisi benar, ini menunjukkan bahwa pengguna admin sedang login.
- Jika pemeriksaan admin lolos, kode tersebut digunakan `header("Location: admin.php")`untuk mengirim header yang mengarahkan browser pengguna ke halaman bernama `admin.php`. Halaman ini kemungkinan besar berisi panel admin atau fungsi yang hanya dapat diakses oleh administrator.
- Jika pemeriksaan admin gagal (artinya status login bukan "login" atau nama pengguna bukan "admin"), kode akan mengeksekusi bagian ini.
- Ia mengirimkan header lain yang digunakan `header('Location: session.php')`untuk mengarahkan pengguna ke halaman bernama `session.php`. Halaman ini dapat berupa formulir login, halaman profil pengguna umum, atau halaman kesalahan yang menunjukkan akses tidak sah.
- Kode tersebut mencakup konten HTML dasar yang mungkin ditampilkan secara kondisional atau tanpa syarat:
- `<h1>Halaman User</h1>`:Ini akan menampilkan judul "Pengguna Halaman" (Bahasa Indonesia untuk "Halaman Pengguna").
- `<h1>Halo, <?= $_SESSION['nama'] ?></h1>`:Ini menampilkan pesan ucapan "Halo," diikuti dengan nilai`nama`(nama) variabel sesi,jika itu ada.
- `<a href="logout.php">Logout</a>`:Ini menciptakan link dengan teks "Logout" yang menunjuk ke halaman bernama`logout.php`,kemungkinan digunakan untuk mengeluarkan pengguna.
# Upload & download

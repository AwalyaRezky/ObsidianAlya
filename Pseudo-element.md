# PSEUDO-ELEMENT 
Pseudo elemen adalah bagian virtual dari elemen HTML yang dapat dipilih dan diubah gaya tampilannya menggunakan CSS. Mereka digunakan untuk memodifikasi atau menambahkan gaya ke bagian-bagian tertentu dari elemen, tanpa harus menambahkan elemen HTML tambahan.

Pseudo elemen ditandai dengan menggunakan tanda titik dua (::) setelah nama elemen dalam aturan CSS. Dua tanda titik dua (::) digunakan untuk pseudo elemen yang diperkenalkan dalam standar CSS3, sedangkan sebuah tanda titik dua (:) digunakan untuk pseudo elemen yang diperkenalkan dalam standar CSS2.

Perbedaan antara standar CSS2 dan CSS3:
1.Waktu Rilis:
- CSS2: CSS2 diterbitkan pada tahun 1998.
- CSS3: CSS3 adalah pengembangan berkelanjutan dari CSS2 dan diperkenalkan secara bertahap sejak tahun 1999. Sebagai standar yang lebih baru, CSS3 terus mengalami penambahan dan pembaruan dari waktu ke waktu.
2.Modul:
- CSS2: CSS2 terdiri dari satu modul utama dan beberapa modul tambahan yang mendefinisikan berbagai fitur dan properti CSS.
 - CSS3: CSS3 dibagi menjadi banyak modul yang berbeda, masing-masing fokus pada aspek tertentu dari desain web. Setiap modul CSS3 berkembang secara independen, yang memungkinkan penambahan fitur baru tanpa harus menunggu rilis keseluruhan.
3.Fitur dan Kemampuan:
- CSS2: CSS2 menyediakan seperangkat fitur dasar yang mencakup pemformatan teks, warna, tata letak, pengelolaan lapisan, dan selektor.
- CSS3: CSS3 memperkenalkan banyak fitur baru yang meliputi efek transisi, animasi, transformasi 2D/3D, bayangan, gradien, tata letak responsif, media queries, dan banyak lagi. CSS3 juga memperkenalkan pseudo elemen yang lebih banyak dan peningkatan dalam selektor CSS.
4.Kompatibilitas Browser:
- CSS2: Mayoritas browser yang digunakan pada saat CSS2 diterbitkan telah mendukung sebagian besar fitur CSS2.
- CSS3: Implementasi fitur CSS3 oleh browser-browser modern beragam. Beberapa fitur CSS3 mungkin tidak didukung secara penuh di semua browser, dan beberapa fitur mungkin memerlukan pr


# Beberapa Contoh Pseudo-Element
## 1. ::Before & ::After 
adalah bagian dari CSS Pseudo-Elements yang memungkinkan Anda untuk menyisipkan konten tambahan sebelum atau setelah konten aktual suatu elemen HTML. Dengan menggunakan pseudo-element ini, Anda dapat menambahkan elemen dekoratif atau konten tambahan ke dalam elemen HTML tanpa harus mengubah struktur HTML itu sendiri.

```css
.custom-button::before {
  content: "🔴 ";
  color: red;
  margin-right: 5px;
}

.custom-button::after {
  content: " 🔴";
  color: red;
  margin-left: 5px;
}
```

## 2. ::First-Letter & ::First-line
### Letter 
::first-letter: Pseudo-elemen ::first-letter digunakan untuk memilih dan memanipulasi huruf pertama dalam teks yang ada di dalam elemen tertentu. Ini memungkinkan Anda menerapkan gaya khusus, seperti ukuran huruf yang lebih besar, jenis huruf yang berbeda, atau warna teks yang berbeda, pada huruf pertama dari kata atau paragraf.

Contoh penggunaan CSS untuk pseudo-elemen ::first-letter:
```css
   p::first-letter {
     font-size: 20px;
     font-weight: bold;
     color: red;
   }
```
Dalam contoh di atas, huruf pertama dari setiap paragraf akan memiliki ukuran huruf 20 piksel, tebal huruf yang lebih tebal, dan warna teks merah.
   
### Line
::first-line: Pseudo-elemen ::first-line digunakan untuk memilih dan memanipulasi baris pertama dalam teks yang ada di dalam elemen tertentu. Ini memungkinkan Anda menerapkan gaya khusus pada baris pertama, seperti mengubah ukuran huruf, gaya teks, atau margin.

Contoh penggunaan CSS untuk pseudo-elemen ::first-line:
```css
   p::first-line {
     font-size: 18px;
     font-style: italic;
     color: blue;
     margin-left: 20px;  
     }
    
```
Dalam contoh di atas, baris pertama dari setiap paragraf akan memiliki ukuran huruf 18 piksel, gaya huruf miring, warna teks biru, dan margin kiri sebesar 20 piksel.
### Kesimpulan
Penting untuk dicatat bahwa pseudo-elemen ::first-letter dan ::first-line hanya dapat digunakan dengan elemen teks seperti `<p>`, `<h1>`, `<span>`, dan sebagainya. Selain itu, dukungan untuk pseudo-elemen ini mungkin bervariasi tergantung pada browser yang digunakan.

## 3. ::Selection 
Pseudo elemen dalam CSS digunakan untuk memanipulasi atau memodifikasi bagian-bagian spesifik dari elemen HTML tertentu. Salah satu pseudo elemen yang sering digunakan adalah ::before dan ::after, yang digunakan untuk menambahkan konten tambahan sebelum atau setelah isi elemen tersebut.

Jika ingin memilih atau memanipulasi teks yang dipilih oleh pengguna, maka kita dapat menggunakan pseudo kelas ::selection. Pseudo kelas ini memungkinkan Anda untuk mengatur gaya teks dan latar belakang teks yang dipilih oleh pengguna di dalam elemen.

Berikut adalah contoh penggunaan pseudo kelas ::selection dalam CSS:

```css
::selection {
  color: white;
  background-color: blue;
}
```

Dalam contoh di atas, ketika pengguna memilih teks di dalam elemen yang menggunakan pseudo kelas ::selection, teks yang dipilih akan memiliki warna teks putih dan latar belakang biru.

Harap diingat bahwa dukungan untuk pseudo kelas ::selection dapat bervariasi di beberapa browser. Jadi, pastikan untuk menguji tampilan pada berbagai browser untuk memastikan konsistensi penampilan.
# Kode Program
```HTML
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="pseudo_element.css">
</head>
<body>
  <div class="card">
    <h2 class="card-title">DANAU TOBA</h2>
    <p class="teks">Pada zaman dahulu adalah seorang petani bernama Toba yang menyendiri di sebuah lembah yang landai dan subur. Petani itu mengerjakan sawah dan ladang untuk keperluan hidupnya.Selain mengerjakan ladangnya, kadang-kadang lelaki Itu pergi memancing ikan ke sungai yang berada takjauh dari rumahnya.Setiap kah dua memancing, mudah saja ikan didapatnya karena di sungai yang jernih itu memang banyak sekali ikan. lkan hasil pancingannya dia masak untuk dimakan</p>
  </div>
</body>
</html>
```

```CSS
.card {
    background-color: #f2f2f2;
    border: 1px solid #ccc;
    padding: 20px;
  }
.card-title::after {
    content: '';
    display: block;
    border-bottom: 2px solid #333;
    margin-top: 8px;
  }
p::first-letter {
    font-size: 28px;
    color: red;
  }
.teks::first-line {
    font-size: 19px;
    color: blue;
  }
::selection {
    color: white;
    background: #333;
  }
```
# Hasil
![gambar](ASET/hasil.png)
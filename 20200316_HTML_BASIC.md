# HTML Dasar

## Definisi HTML
HTML(*Hyper Text Markup Language*) adalah markup *language* yang mana mendefinisakn struktur dari sebuah konten. HTML terdiri dari serangkaian element yang digunakan untuk melampirkan, atau membungkus, berbagai bagian dari konten untuk membuatnya muncul dengan cara tertentu, atau bertindak dengan cara tertentu. Melampirkan tag dapat membuat hyperlink text atau gambar merujuk ke alamat lain, dapat membuat kata-kata huruf miring, dapat membuat font lebih besar atau lebih kecil, dan sebagainya. Sebagai contoh jika ingin agar baris berdiri sendiri, dapat menentukan bahwa itu adalah paragraf dengan melampirkannya dalam tag paragraf:

````
<p>ini adalah kalimat paragraf.</p>
````


## Elemen-Elemen di dalam HTML
Struktur elemen pada HTML:

1. Tag pembuka: Terdiri dari nama elemen, dibungkus dengan kurung sudut buka dan tutup(contoh: `<p>`). Ini menyatakan di mana elemen dimulai atau mulai berlaku - dalam kasus diatas ini di mana paragraf dimulai.
2. Tag penutup: Sama seperti tag pembuka, bedanya, pada tag penutup terdapat garis miring di depan nama elemen. Ini menyatakan di mana elemen berakhir dalam hal ini di mana paragraf berakhir. Gagal menambahkan tag penutup adalah salah satu kesalahan standar pemula dan dapat menyebabkan hasil yang aneh.
3. Konten: adalah konten elemen, yang dalam hal contoh di atas adalah teksnya.
4. Elemen: Tag pembuka, tag penutup serta konten bersama-sama adalah sebuah elemen.

### Nesting Element (Elemen di dalam elemen)
Dalam HTML elemen bisa diletakkan di dalam elemen lain dengan kata lain bersarang. Jika ingin menyatakan bahwa dia sangat pemarah, dengan membungkus kata "sangat" dalam elemen `<strong>`, berarti bahwa kata tersebut harus ditekankan dengan kuat:
````
<p> Dia <strong> sangat </strong> kasar.</p>
````
hasil:
<p> Dia <strong> sangat </strong> kasar.</p>


### Empty Element
Beberapa elemen tidak memiliki konten dan disebut elemen kosong. Sebagai contoh lihat elemen <img> di bawah ini:
````
<img src="images/firefox-icon.png" alt="My test image">
````
Ini berisi dua atribut, tetapi tidak ada tag </img> penutup dan tidak ada konten di dalamnya. Ini karena elemen gambar tidak membungkus konten untuk mempengaruhinya. Tujuannya adalah untuk menanamkan gambar di halaman HTML.

berikut adalah contoh-contoh empty elemen HTML:
1. `<area>` = fungsinya untuk mendefinisikan area pada image map. Image map merupakan sebuah gambar yang memiliki area yang bisa diklik Tag `<area>` selalu berada di dalam tag `<map>`.
2. `<input>` = Tag `<input>` fungsinya untuk membuat elemen input pada form. Tag ini memiliki atribut type yang akan menentukan jenis inputannya.
3. `<link>` = Tag `<link>` digunakan untuk mendefinisikan hubungan antara dokumen HTML dengan resource eksternal seperti CSS. Tag ini juga bisa digunakan untuk membuat favicon.
4. `<meta>` = Tag `<meta>` digunakan untuk mendefinisikan Metadata sebuah halaman web. Metadata tidak akan ditampilkan pada halaman web, melainkan akan dibaca oleh mesin atau Bot (robot). Tag `<meta>` ini penting untuk SEO (search engine optimization). Jadi, kalau membuat web tanpa menggunakan tag `<meta>`, kemungkinan akan sulit terindeks oleh mesin pencari.
5. DLL.

### Anatomi dokumen HTML
````
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>My test page</title>
  </head>
  <body>
    <img src="images/firefox-icon.png" alt="My test image">
  </body>
</html>
````

penjelasan:
- `<! DOCTYPE html>` - doctype. Diperlukan mukadimah. Dalam kabut waktu, ketika HTML masih muda (sekitar 1991/92), DOCTYPE dimaksudkan untuk bertindak sebagai tautan ke serangkaian aturan yang harus diikuti oleh halaman HTML untuk dianggap sebagai HTML yang baik, yang bisa berarti pengecekan kesalahan otomatis dan lainnya. hal yang bermanfaat. Namun hari ini, mereka tidak berbuat banyak, dan pada dasarnya hanya diperlukan untuk memastikan dokumen Anda berperilaku dengan benar. Hanya itu yang perlu Anda ketahui untuk saat ini.
- `<html> </html>` - elemen `<html>`. Elemen ini membungkus semua konten di seluruh halaman dan kadang-kadang dikenal sebagai elemen root(akar).
- `<head> </head>` - elemen `<head>`. Elemen ini bertindak sebagai wadah untuk semua hal yang ingin Anda sertakan pada halaman HTML yang bukan konten yang Anda tampilkan kepada pengunjung halaman Anda. Ini termasuk hal-hal seperti kata kunci dan deskripsi halaman yang ingin Anda tampilkan di hasil pencarian, CSS untuk menata konten kami, deklarasi set karakter dan banyak lagi.
didalam blok head terdapat `<title>` dan `<h1>` berikut bedanya:
    - Elemen `<h1>` muncul di halaman saat dimuat di browser - umumnya `<h1>` harus digunakan sekali per halaman, untuk menandai judul konten halaman (judul cerita, atau berita utama, atau apa pun yang sesuai dengan penggunaan. )
    - Elemen `<title>` adalah metadata yang mewakili judul keseluruhan dokumen HTML (bukan konten dokumen.)
- `<meta charset = "utf-8">` - Elemen ini mengatur karakter set dokumen Anda harus digunakan untuk UTF-8 yang mencakup sebagian besar karakter dari sebagian besar bahasa manusia. Pada dasarnya, sekarang dapat menangani konten teks yang mungkin Anda masukkan ke dalamnya. Tidak ada alasan untuk tidak mengatur ini dan ini dapat membantu menghindari beberapa masalah di kemudian hari.
- `<title> </title>` - elemen `<title>`. Ini mengatur judul halaman Anda, yang merupakan judul yang muncul di tab browser tempat halaman itu dimuat. Ini juga digunakan untuk menggambarkan halaman ketika Anda membookmark / favoritnya.
- `<body> </body>` - elemen `<body>`. Ini berisi semua konten yang ingin Anda tunjukkan kepada pengguna web ketika mereka mengunjungi halaman Anda, apakah itu teks, gambar, video, game, trek audio yang dapat diputar atau apa pun.

### List
#### Unlist Order
*Unlist order* adalah untuk daftar yang urutan barangnya tidak penting, seperti daftar belanja. Ini dibungkus dengan elemen `<ul>`. contoh:
````
    <ul>
        <li>Items List</li>
        <li>Unit List</li>
        <li>Transactions List</li>
        <li>Stock List</li>
     </ul>
````

dan akan menghasilkan seperti ini:
<ul>
        <li>Items List</li>
        <li>Unit List</li>
        <li>Transactions List</li>
        <li>Stock List</li>
     </ul>

#### Ordered List
*Ordered List* adalah untuk daftar yang urutannya penting, seperti resep. Ini dibungkus dalam elemen `<ol>`.
```` 
 <ol>
    <li>Langkah 1</li>
    <li>Langkah 2</li>
    <li>Langkah 3</li>
    <li>Langkah 4</li>
 </ol>
````
dan akan menghasilkan seperti ini:
  <ol>
                <li>Langkah 1</li>
                <li>Langkah 2</li>
                <li>Langkah 3</li>
                <li>Langkah 4</li>
</ol>

### Table
Elemen HTML `<table>` mewakili data tabular - yaitu, informasi yang disajikan dalam tabel dua dimensi yang terdiri dari baris dan kolom sel yang berisi data.
contoh table:
````
<table border="1">
            <tr>
                <th>ID</th>
                <th>item</th>
                <th>quantity</th>
                <th>unit</th>
            </tr>
            <tr>
                <td>1</td>
                <td>beras</td>
                <td>150</td>
                <td>g</td>
            </tr>
             <tr>
                <td>1</td>
                <td>garam</td>
                <td>1</td>
                <td>kg</td>
            </tr>
</table>
````
hasil:

<table border="1">
            <tr>
                <th>ID</th>
                <th>item</th>
                <th>quantity</th>
                <th>unit</th>
            </tr>
            <tr>
                <td>1</td>
                <td>beras</td>
                <td>150</td>
                <td>g</td>
            </tr>
            <tr>
                <td>1</td>
                <td>garam</td>
                <td>1</td>
                <td>kg</td>
            </tr>
</table>


`<th>` header tabel Sel header di `<table>`.
`<td>` data tabel Sel data dalam `<table>`.

#### Span Column and Row
Baik colspan = dan rowspan = adalah atribut dari dua elemen sel tabel, `<th>`dan `<td>`. Mereka menyediakan fungsionalitas yang sama dengan "menggabungkan sel" dalam program spreadsheet seperti Excel.
contoh untuk colspan:
````
<table> 
    <caption>Nilai Student</caption> 
    <tr> <th colspan="2">student 1</th>
        <th colspan="2">student 2</th>
    </tr> 
    <tr>
        <th>MTK</th>
        <th>IPA</th>
        <th>MTK</th>
        <th>IPA</th> 
    </tr> 
    <tr> 
        <td>82</td>
        <td>85</td>
        <td>78</td>
        <td>82</td>
    </tr> 
</table>
````

hasil:

<table> 
    <caption>Nilai Student</caption> 
    <tr> <th colspan="2">student 1</th>
        <th colspan="2">student 2</th>
    </tr> 
    <tr>
        <th>MTK</th>
        <th>IPA</th>
        <th>MTK</th>
        <th>IPA</th> 
    </tr> 
    <tr> 
        <td>82</td>
        <td>85</td>
        <td>78</td>
        <td>82</td>
    </tr> 
</table>


contoh untuk rowspan:
````
<table>
 <tr>
  <th>Nama Item</th>
  <th>Jenis</th>
 </tr>
 <tr>
    <td>indomie</td>
    <td rowspan="2">instant</td>
 </tr>
 <tr>
     <td>popmie</td>
</tr>
<tr>
    <td>rendang</td>
    <td rowspan="2">non instant</td>
</tr>
<tr>
    <td>gulai</td>
</tr>
</table>
````
hasil:
<table>
 <tr>
  <th>Nama Item</th>
  <th>Jenis</th>
 </tr>
 <tr>
    <td>indomie</td>
    <td rowspan="2">instant</td>
 </tr>
 <tr>
     <td>popmie</td>
</tr>
<tr>
    <td>rendang</td>
    <td rowspan="2">non instant</td>
</tr>
<tr>
    <td>gulai</td>
</tr>
</table>

### Form
Elemen HTML `<form>` mewakili bagian dokumen yang berisi kontrol interaktif untuk mengirimkan informasi.
contoh:
````
<form action="" method="get" class="form-example">
  <div class="form-example">
    <label for="name">Enter name of item: </label>
    <input type="text" name="item-name" id="item-name" required>
  </div>
  <div class="form-example">
    <label for="email">Enter name of unit: </label>
    <input type="email" name="unit-name" id="unit-name" required>
  </div>
  <div class="form-example">
    <input type="submit" value="add">
  </div>
</form>
````


## Struktur Website HTML yang Tepat
Hal paling umum yang akan dimiliki pada proyek situs web apa pun adalah file *index* HTML dan folder yang berisi gambar, file gaya, dan file *script*. Mari kita buat ini sekarang:

- **index.html**: File ini umumnya akan berisi konten beranda Anda, yaitu teks dan gambar yang dilihat orang ketika mereka pertama kali pergi ke situs Anda. Menggunakan editor teks Anda, buat file baru bernama index.html dan simpan tepat di dalam folder situs percobaan Anda.
- **folder image**: Folder ini akan berisi semua gambar yang Anda gunakan di situs Anda. Buat folder yang disebut gambar, di dalam folder situs uji Anda.
- **folder style**: Folder ini akan berisi kode CSS yang digunakan untuk menata konten Anda (misalnya, mengatur teks dan warna latar belakang). Buat folder bernama gaya, di dalam folder situs percobaan Anda.
- **folder script**: Folder ini akan berisi semua kode JavaScript yang digunakan untuk menambahkan fungsionalitas interaktif ke situs Anda (mis. tombol yang memuat data saat diklik). Buat folder yang disebut skrip, di dalam folder situs pengujian Anda.








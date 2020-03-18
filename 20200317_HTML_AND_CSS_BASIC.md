# Apa itu Web Forms ?

Formulir web adalah salah satu poin utama interaksi antara pengguna dan situs web atau aplikasi. Formulir memungkinkan pengguna untuk memasukkan data, yang umumnya dikirim ke server web untuk diproses dan disimpan,natau digunakan pada sisi klien untuk segera memperbarui antarmuka dengan beberapa cara (misalnya, tambahkan item lain ke daftar, atau tampilkan atau sembunyikan fitur UI).
Formulir HTML web terdiri dari satu atau lebih kontrol formulir (widget), ditambah beberapa elemen tambahan untuk membantu struktur keseluruhan formulir - mereka sering disebut sebagai bentuk HTML. Kontrol dapat berupa bidang teks tunggal atau multi-baris, kotak dropdown, tombol, kotak centang, atau tombol radio, dan sebagian besar dibuat menggunakan elemen `<input>`.

### Menerapkan HTML formulir

Kita akan menggunakan elemen HTML berikut: `<form>`, `<label>`, `<input>`, `<textarea>` dan `<button>`.

- Elemen Form
```
<form action="/my-handling-form-page" method="post">

</form>
```
Elemen ini secara formal mendefinisikan suatu form. Ini adalah elemen wadah seperti elemen `<section>` atau `<footer>`, tetapi khusus untuk berisi formulir, juga mendukung beberapa atribut spesifik untuk mengonfigurasinya. Semua atributnya adalah opsional, tetapi merupakan praktik standar untuk selalu menetapkan atribut `action` dan `method`:
Atribut `action` menentukan lokasi (URL) tempat data yang dikumpulkan formulir harus dikirim ketika dikirimkan.
Atribut `method` menentukan metode HTTP untuk mengirim data (biasanya dapatkan atau posting).

- Elemen ```<label>, <input>, <textarea> dan <button>```

Bagian entri data berisi tiga bidang teks, masing-masing dengan `<label>` yang sesuai: <br>
Bidang input untuk nama adalah bidang teks satu baris, bidang input untuk email adalah input tipe email: bidang teks satu baris yang hanya menerima alamat email, dan bidang input untuk pesan adalah `<textarea>`bidang teks multiline.
~~~~ html
<form action="/my-handling-form-page" method="post">
 <ul>
  <li>
    <label for="name">Name:</label>
    <input type="text" id="name" name="user_name">
  </li>
  <li>
    <label for="mail">E-mail:</label>
    <input type="email" id="mail" name="user_mail">
  </li>
  <li>
    <label for="msg">Message:</label>
    <textarea id="msg" name="user_message"></textarea>
  </li>
 </ul>
</form>
~~~~

Pada elemen `<input>`, atribut yang paling penting adalah atribut type. Atribut ini sangat penting karena mendefinisikan cara elemen `<input>`
~~~ html
<input type="text" value="by default this element is filled with this text"
~~~

jika ingin menentukan nilai default untuk `<textarea>`, kita dapat menempatkannya di antara tag pembuka dan penutup dari elemen `<textarea>`, seperti ini:
~~~ html
<textarea>
by default this element is filled with this text
</textarea>
~~~

- Elemen `<button>`
Merupakan tombol yang dapat diklik, ini dilakukan dengan menggunakan elemen `<button>` kemudian tambahkan tepat di atas tag `</ul>` penutup:
~~~ html
<li class="button">
  <button type="submit">Send your message</button>
</li>
~~~

### Basic form styling

HTML `<style>` element digunakan untuk menyisipkan kode style atau CSS ke dalam sebuah dokumen web (HTML).
`<style>` element ditulis di dalam element `<head>..</head>` yang merupakan bagian kepala sebuah dokumen HTML. Apabila dituliskan attribute scoped, maka penempatannya boleh ditulis di bagian manapun di dalam element HTML, yang mana `<style>` tersebut hanya berlaku dalam lingkup element itu sendiri.Elemen style merupakan satu dari berbagai cara yang dapat digunakan untuk mengaplikasikan style atau kode CSS kedalam HTML.

~~~ html
<form>
  <fieldset>
    <legend>Fruit juice size</legend>
    <p>
      <input type="radio" name="size" id="size_1" value="small">
      <label for="size_1">Small</label>
    </p>
    <p>
      <input type="radio" name="size" id="size_2" value="medium">
      <label for="size_2">Medium</label>
    </p>
    <p>
      <input type="radio" name="size" id="size_3" value="large">
      <label for="size_3">Large</label>
    </p>
  </fieldset>
</form>
~~~

### Labels are clickable

Seperti yang kita lihat di artikel sebelumnya, `<label>` Elemen adalah cara formal untuk mendefinisikan label untuk widget bentuk HTML. Ini adalah elemen yang paling penting jika Anda ingin membangun formulir yang dapat diakses - ketika diimplementasikan dengan benar. Contoh 

~~~ html 
<label for="name">Name:</label> <input type="text" id="name" name="user_name">
~~~

Dengan `<label>` dikaitkan dengan benar `<input>` melalui foratributnya (yang berisi atribut `<input>`elemen id), user akan membaca "Nama, edit teks".

Ada cara lain untuk mengaitkan kontrol bentuk dengan label bersarang dengan kontrol dalam bentuk `<label>`.
~~~ html
<label for="name">
  Name: <input type="text" id="name" name="user_name">
</label>
~~~

# CSS

CSS (*Cascade Style Sheet*) meruapakan sebuah bahasa untuk mengatur tampilan web sehingga terlihat lebih menarik dan indah. Dengan CSS, kita dapat mengatur layout (tata letak), warna, font, garis, dan lain-lain.

Struktur kode CSS terdiri dari tiga bagian:
1. Selektor;
2. Blok Deklarasi;
3. Properti dan nilanya

- Selektor
Selektor adalah kata kunci untuk memilih elemen HTML yang akan kita atur.
Contohnya:
~~~~ css
h1 {
    color: red;
}
~~~~ 
Artinya: Kita memilih semua elemen `<h1>`, lalu diberikan warna teks red (merah).
Selektor dapat berupa nama *tag, class, id, dan atribut*.
Contoh:
~~~ css
/* Selektor dengan nama tag */
h2 {
    color: blue
}

/* Selektor degnan class */
.bg-yellow {
    backgound-color: yellow;
}

/* selektor dengan ID elemen */
#header {
    background: grey;
}

/* Selektor dengan Atribut */
input[type=text]{
    background: yellow;
}
~~~

- Blok Deklarasi

Blok deklarasi adalah tempat kita menuliskan atribut-atibut CSS yang akan diberikan ke pada selektor.
Contoh:
~~~ css
p {
    font-size: 18px;
}
~~~

Artinya, kita akan mengatur ukuran font dari tag `<p>` sebesar `18px`.
Blok deklarasi dimulai atau dibuka dengan tanda kurung `{` lalu ditutup dengan `}`.


- Properti dan Nilainya

Properti merupakan atribut atau sekumpulan aturan yang akan diberikan kepada elemen yang dipilih.
`properti: "nilai"`

Setiap properti harus diakhiri dengan titik koma. Apabila hanya terdapat satu properti, boleh tidak menggunakan titik koma.
Properti harus ditulis di dalam blok deklarasi.
Contoh:
~~~ css
blockquote {
    background: pink;
}
~~~


#### Cara Menulis kode CSS dalam HTML

Penulisan kode CSS di HTML dapat dilakukan di dalam tag `<style>`. Tag tersebut dapat ditulis di dalam tag `<head>` atau `<body>`.
Bisa juga dituliskan di dalam tag <head>. Perhatiakn contoh berikut ini:
~~~~ html
<!DOCTYPE html>
<html>
<head>
<title>Contoh Penulisan kode CSS</title>

<style type="text/css">
    p { color: red }
</style>

</head>

<body>
    <p>Sebuah contoh paragraf yang sudah diberikan oleh kode CSS</p>
</body>
</html>
~~~~ 

#### Penulisan CSS dalam Html

Penulisan kode CSS dalam HTML dibagi menjadi tiga cara *internal, inline, dan eksternal*. Pembagian ini berdasarkan letak kode CSS tersebut ditulis.

- Internal CSS

Internal CSS adalah kode CSS yang ditulis di dalam tag `<style>`. Internal CSS juga dikenal dengan sebutan Embeded CSS.
Tag `<style>` biasanya ditulis di dalam tag `<head>`. Bisa juga ditulis di dalam `<body>`, namun lebih banyak ditulis di dalam `<head>`.

~~~~ html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Transaction Form</Form></title>
    <style>
        form {
            margin: 0 auto;
            width: 400px;
            padding: 1em;
            border: 1px solid #CCC;
            border-radius: 1em;
        }

        ul {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        form li + li {
            margin-top: 1em;
        }

        label {
            display: inline-block;
            width: 90px;
            text-align:right;
        }
        .button {
            padding-left: 90px;
        }

        button {
            margin-left: .5em;
        }
    </style>

  </head>
<body>
    <header>
        <h1>Unit Form</h1>
    </header>   
  <nav>
    <ul>
      <li><a href=".../../../index.html">Home</a></li>
      <li><a href="../Items/index.html">Item</a></li>
      <li><a href="../Units/index.html">Unit</a></li>
      <li><a href="../Stocks/index.html">Stock</a></li>
    </ul>
   </nav>
   <br><br><br>
   <main>
       <form action="../index.html"method="post">
       <ul>
           <li>
               <label>ID : </label><br>
               <label for="name">Name :</label>
               <input type="text" id="name" name="name"><br>
               <label for="description">Description :</label>
               <input type="text" id="description" name="description">
           </li>
          <li>
              <li class ="button">
          <button type="submit">save</button>
          </li>
       </ul>
    </form>
    <a href = "../Units/index.html">Back</a>
     </main>
    </body>
</html>
~~~~

- Eksternal CSS

Eksternal CSS adalah kode CSS yang ditulis terpisah dengan kode HTML. Eksternal CSS ditulis disebuah file khusus yang berekstensi .css. Sebagai contoh, styles.css

~~~~ css
form ul {
        margin: 0 auto;
        width: 400px;
        padding: 1em;
        border: 1px solid #CCC;
        border-radius: 1em;
    }

    form ul {
        list-style: none;
        padding: 0;
        margin: 0;
    }

    form li + li {
        margin-top: 1em;
    }

    label {
        display: inline-block;
        width: 90px;
        text-align:right;
    }
    li.button {
        padding-left: 90px;
    }
    
    button {
        margin-left: .5em;
    }
~~~~

Untuk menggunakan CSS tersebut dalam HTML, kita perlu mengimpornya. Ada beberapa cara memasukkan kode CSS dari berkas eksternal:

Pertama menggunakan tag `<link>`
~~~ html
<link rel="stylesheet" type="text/css" href="../assets/styles.css">
~~~

penulisan pada HTML nya adalah 
~~~~ html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Transaction Form</Form></title>
    
    <link rel =<link rel="stylesheet" href="../assets/stlyes/form.css">
    <link rel =<link rel="stylesheet" href="../assets/stlyes/styles.css">
  </head>
<body>
    <header>
        <h1>Transaction Form</h1>
    </header>
    .
    .
    .
</body>
</html>
~~~~




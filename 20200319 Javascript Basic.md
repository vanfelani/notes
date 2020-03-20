# Javascript basic
![](https://velocitydeveloper.com/wp-content/uploads/2019/04/Javascript.jpg)

JavaScript adalah bahasa scripting atau pemrograman yang memungkinkan Anda untuk mengimplementasikan fitur kompleks pada halaman web

Bahasa javascript client-side ini terdiri dari beberapa fitur pemrograman umum yang memungkinkan Anda melakukan hal-hal seperti: <br>
   - Menyimpan nilai yang berguna di dalam variabel. Dalam contoh di atas misalnya, kami meminta nama baru untuk dimasukkan kemudian menyimpan nama itu dalam variabel yang disebut name .
   - Operasi pada potongan teks (dikenal sebagai "string" dalam pemrograman). Pada contoh di atas kita mengambil string "Player 1:" dan bergabung dengan variabel name untuk membuat label teks lengkap, misalnya '' Player 1: Chris ".
   - Menjalankan kode sebagai respons terhadap peristiwa tertentu yang terjadi pada halaman web. Kami menggunakan acara click dalam contoh kami di atas untuk mendeteksi kapan tombol diklik dan kemudian menjalankan kode yang memperbarui label teks.
   - Dan banyak lagi! 

   Namun yang lebih menarik adalah fungsionalitas yang dibangun di atas bahasa JavaScript sisi klien. Apa yang disebut Application Programming Interfaces ( APIs ) memberi Anda kekuatan super tambahan untuk digunakan dalam kode JavaScript Anda.

   API adalah set blok pembangun kode yang siap pakai yang memungkinkan pengembang mengimplementasikan program yang sulit atau tidak mungkin dilaksanakan. Mereka melakukan hal yang sama untuk pemrograman yang dilakukan oleh kit furnitur siap pakai untuk pembangunan rumah - jauh lebih mudah untuk mengambil panel yang sudah jadi dan menyatukannya untuk membuat rak buku daripada mengerjakan sendiri desainnya, pergi dan temukan perbaiki kayu, potong semua panel dengan ukuran dan bentuk yang tepat, temukan sekrup berukuran benar, lalu satukan untuk membuat rak buku.

JavaScript APIs mempunyai 2 Kategori :
1. browser API <br>
    ibuat di dalam peramban web Anda, dan dapat mengekspos data dari lingkungan komputer di sekitarnya, atau melakukan hal-hal rumit yang bermanfaat, 
    contoh :
    - DOM API<br>
        memungkinkan Anda untuk memanipulasi HTML dan CSS, membuat, menghapus dan mengubah HTML, secara dinamis menerapkan gaya baru ke halaman Anda, dll. Setiap kali Anda melihat jendela sembulan muncul di halaman, atau beberapa konten baru yang ditampilkan (seperti yang kita lihat di atas dalam demo sederhana kami) misalnya, itulah DOM yang sedang beraksi.
    - Geolocation API :<br>
        mengambil informasi geografis. Ini adalah cara Google Maps menemukan lokasi Anda dan memplotnya di peta.
    -  Canvas dan WebGL<br>
        memungkinkan Anda membuat gambar animasi 2D dan 3D. Orang-orang melakukan beberapa hal luar biasa menggunakan teknologi web ini — lihat Eksperimen Chrome dan contoh web .
    - API Audio dan Video seperti HTMLMediaElement dan WebRTC <br>
        memungkinkan Anda melakukan hal-hal yang sangat menarik dengan multimedia, seperti memutar audio dan video langsung di halaman web, atau mengambil video dari kamera web Anda dan menampilkannya di komputer orang lain (coba demo Snapshot sederhana kami) untuk mendapatkan ide).

1. Third party API <br>
     Tidak dibangun ke dalam browser secara default, dan Anda umumnya harus mengambil kode dan informasi mereka dari suatu tempat di Web. Sebagai contoh:
    - Twitter API memungkinkan Anda melakukan hal-hal seperti menampilkan tweet terbaru Anda di situs web Anda.
    - Google Maps API dan OpenStreetMap API memungkinkan Anda untuk menyematkan peta khusus ke situs web Anda, dan fungsionalitas lainnya. 

    JavaScript dieksekusi oleh mesin JavaScript browser, setelah HTML dan CSS telah dirakit dan disatukan ke dalam halaman web. Ini memastikan bahwa struktur dan gaya halaman sudah ada pada saat JavaScript mulai berjalan.
    Javascript menjalankan blok javascript dari atas ke bawah dengan compile Interpreted.

    Kode Client Side adalah kode yang dijalankan di komputer pengguna - ketika halaman web dilihat, kode Client Side halaman diunduh, kemudian jalankan dan ditampilkan oleh browser. Dalam modul ini kita secara eksplisit berbicara tentang JavaScript Client Side, namun ada juga Javascript yang berjalan Server Side seperti Node Js.

    JavaScript Client Side secara dinamis menghasilkan konten baru di dalam browser pada klien, misalnya membuat tabel HTML baru, mengisinya dengan data yang diminta dari server , lalu menampilkan tabel di halaman web yang ditunjukkan kepada pengguna. Maknanya sedikit berbeda dalam dua konteks, tetapi terkait, dan kedua pendekatan (server side dan client side) biasanya bekerja bersama.

    Halaman web tanpa konten yang diperbarui secara dinamis disebut statis - hanya menampilkan konten yang sama setiap saat. 

Cara menambahkan Javascript kedalam halaman web bisa dengan 2 Cara :

1. - Internal javascript
    Memasukkan javascript didalam halaman.
    ```
    <head>
        <script>
            console.log("Hello");
        </script>
    </head>
    ```
1. - External Script
    kita menjalankan javascript namun difile yang terpisah .

    ```
        script.js
    ```

    Menjalankan di html

    ```
    <script src="script.js" defer></script>
    ```

- Fitur Async dan defer <br>
    - async adalah mendownload skrip tanpa memblokir rendering halaman dan akan menjalankannya segera setelah skrip selesai mengunduh. Anda tidak mendapatkan jaminan bahwa skrip akan berjalan dalam urutan tertentu, hanya saja skrip tersebut tidak akan menghentikan tampilan halaman lainnyaada blank, Contoh :<br>
    ```
        <script async src = "js / vendor / jquery.js"> </script>
        <script async src = "js / script2.js"> </script>
        <script async src = "js / script3.js"> </script> 
    ```
    - defer adalah attribut yang berjalan sesuai urutan yang muncul di halaman dan menjalankannya segera setelah skrip dan konten diunduh, Contoh :<br>
    ```
     <script defer src = "js / vendor / jquery.js"> </script>
     <script defer src = "js / script2.js"> </script>
     <script defer src = "js / script3.js"> </script> 
    ```

    Intinya async dan defer keduanya menginstruksikan browser untuk mengunduh skrip di utas terpisah, sedangkan halaman lainnya (DOM, dll.) sedang mengunduh, sehingga pemuatan halaman tidak diblokir oleh skrip. Jika Script anda harus segera dijalankan dan script tersebut tidak memiliki depedency maka gunakan async dan jika script anda harus menunggu penguraian dan bergantung pada script lain atau dom yang ada maka gunakan defer

- Komentar dalam javascript hampir sama dengan Java, contoh :
    ```
        //komen 1 baris
        /*
         komen lebih dari 1 baris
        */
    ```

- Undefined vs Null
    1. Undefined adalah keyword khusus lainnya di dalam JavaScript yang mengindikasikan ’tidak ada nilai’. Namun undefined lebih ’dalam’ dari pada null. <br>
    1. Null adalah kata kunci (keyword) khusus yang berarti ‘tidak memiliki nilai’. Kita bisa memberikan nilai null kepada variabel, elemen dari array, property dari objek, atau yang lainnya.


- Variabel Javascript adalah sebuah nama yang mewakili sebuah nilai.    Variabel bisa diisi dengan berbagai macam nilai seperti string (teks), number (angka), objek, array, dan sebagainya. Cara membuat Variabel bisa dengan 2 cara yaitu Var dan Let Contoh : <br>
```
    var a = 1;
    let b = 1;
```
var adalah memiliki 2 variabel bisa namun variable yang sebelumnya akan ditimpa, sedangkan let terbalik dengan var dan const sama dengan konstanta nilainya tidak bisa dirubah.


- Konstanta Javascript adalah sebuah nama yang mewakili sebuah nilai, sama dengan variabel namun nilainya tidak bisa berubah-ubah, contoh:<br>
```
    const a = 1;
```

- Tipe data adalah jenis-jenis data yang bisa kita simpan di dalam variabel. <br>
    Ada beberapa tipe data dalam pemrograman Javascript:

    - String (teks)
    - Integer atau Number (bilangan bulat)
    - Float (bilangan Pecahan)
    - Boolean (True dan False)
    - Object
cara untuk mengetahui sebuat tipe data bisa dengan menggunakan function typeof(), contoh :
```
    let a = 1;
    console.log(typeof(a));
```
- Operator adalah simbol yang digunakan untuk melakukan operasi pada suatu nilai dan variabel.

ada 6 Operator didalam Javascript :
1.   Operator aritmatika<br> merupakan operator untuk melakukan operasi aritmatika seperti penjumlahan, pengurangan, pembagian, perkalian, dsb.
contoh : <br>

     *, +, -, /, %.
1.   Operator Penugasan (Assignment)<br> operator yang digunakan untuk memberikan tugas kepada variabel. Biasanya digunakan untuk mengisi variabel.
contoh : <br> 

        =, +=, -=, *=, /=.

1.   Opeartor relasi atau perbandingan<br>adalah operator yang digunakan untuk membandingkan dua nilai.
contoh :<br> 
<, >, ==, !=, <=, >=
1.   Operator Logika digunakan untuk melakukan operasi terhadap dua nilai boolean. contoh :<br> 
&&, ||, !.
1.   Operator Bitwise merupkan operator yang digunakan untuk operasi berdasarkan bit (biner). contoh :<br> 
&, |, ^, dll.
1.   Operator Ternary merupakan operator yang teridiri dari tiga bagian.
contoh : <br>
(kondisi) ? "Benar" : "salah";

- Pengkondisian
    - if
        ```
        if(kondisi) {

        } 
    - if else
        ```
        if(kondisi) {

        }else {

        }
    - if else if else
        ```
        if(kondisi) {

        } else if(kondisi2) {

        } else {

        }
    - switch case
        ```
        switch(kondisi) {
            case 1 : 
                break;
            case 2 :
                break;
            default :
                break;
        }
- Pengulangan
    - for
        ```
        for(let i = 0; i<=10; i++) {

        }
    - while
        ```
        let i = 0;
        while(i <= 10) {

            i++
        }
    - do while
        ```
        let i = 0;
        do{

            i++;
        }while(i <= 10);h

- Array merupakan struktur data yang digunakan untuk menyimpan sekumpulan data dalam satu tempat.<br>
    - Deklarasi Array dalam Javascript :
        ```
        var products = ["Flashdisk", "SDD", "Monitor"];
    - Memanggil Array dalam javascript :
        ```
        products[1]; //menampilkan data SSD
- Objek adalah sebuah variabel yang menyimpan nilai (properti) dan fungsi (method), contoh syntax Object :<br>
    ```
        var car = {
            // properti
            type: "Fiat", 
            model: "500", 
            color: "white",

            // method
            start: function(){
                console.log("ini method start");
            },
            drive: function(){
                console.log("ini method drive");
            },
            brake: function(){
                console.log("ini method brake");
            },
            stop: function(){
                console.log("ini method stop");
            }
            
        };
    ```
    - Cara mengakses properti dan method object :<br>
    Caranya menggunakan tanda titik atau dot (.), lalu diikuti dengan nama properti atau method. <br>
         ```
        console.log(car.type);
        console.log(car.color);

        car.start();
        car.drive();
        ```
    - Cara menggunakan keyword this<br>
    Kata kunci this digunakan untuk mengakses properti dan method dari dalam method (objek), contoh :<br>
        ```
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <meta http-equiv="X-UA-Compatible" content="ie=edge">
            <title>Belajar Objek Javascript</title>

        <script>
            var person = {
                firstName: "Muhar",
                lastName: "Dian",
                showName: function(){
                    alert(`Nama: ${this.firstName} ${this.lastName}`);
                }
            };

            person.showName(); //kata kunci this mengacu pada objek person.
        </script>
        </head>
        <body>
        ```
    - Cara membuat class object dengan this<br>
        Pada pemrograman berorientasikan objek, kita biasanya membuat objek dengan membuat instance dari class.
        Pada Javascript versi ES5, class belum ada. Fitur ini baru ditambahkan pada Javascript versi ES6.
        Pada ES5, kita bisa membuat class dengan fungsi. Lalu di dalamnya menggunakan kata kunci this. 
        
        contoh :<br>
        ```
            <!DOCTYPE html>
            <html lang="en">
            <head>
                <meta charset="UTF-8">
                <meta name="viewport" content="width=device-width, initial-scale=1.0">
                <meta http-equiv="X-UA-Compatible" content="ie=edge">
                <title>Belajar Objek Javascript</title>

            <script>
                function Person(firstName, lastName){
                    // properti
                    this.firstName = firstName;
                    this.lastName = lastName;

                    // method
                    this.fullName = function(){
                        return `${this.firstName} ${this.lastName}`
                    }
                    this.showName = function(){
                        document.write(this.fullName());
                    }
                }

                var person1 = new Person("Muhar", "Dian");
                var person2 = new Person("Petani", "Kode");

                person1.showName();
                document.write("<br>");
                person2.showName();
            </script>
        </head>
        <body>
        ```

        Kita membuat objek baru dengan kata kunci new, lalu diberikan nilai parameter firstName dan lastName.
        ```
        var person1 = new Person("Muhar", "Dian");
        ```
        Jadi berapapun object yang ingin kita buat, cukup gunakan kata new.

- Function vs Method
  - Function adalah sebuah statement yang dibuat di dalam blok dengan cara penulisan yang telah ditentukan, agar dapat digunakan terus menerus. Sehingga tidak ada penulisan code yang berulang.
  contoh :<br>
  ```
  function nama_function() {
      //isi functionnya
  }

  nama_function();//memanggil dan menjalankan function
  ```
  - method adalah statement blok yang didefinisikan di dalam sebuah class. dan javascript menyediakan beberapa fungsi method.
  contoh : <br>
    ```
    <script>
    var arr1 = [];
        console.log(arr1.join()); //menggunakan method join()
    </script>


- Function Anonymous
    adalah sebuah fungsi yang tidak memiliki nama, fungsi yang disimpan dalam variabel tidak perlu nama fungsi. mereka selalu dipanggil (dipanggil) menggunakan nama variabel.
    contoh :<br>
    ```
    var x = function (a, b) {return a * b};
    var z = x(4, 3); 

- Function Scope
    Adalah saat kita membuat sebuah function baru, maka hak ases terhadap function tersebut tidak bisa digunakan oleh statement diluar function yang baru dibuat,
    contoh :<br>
    ```
        const a2plusb2 = (a, b) => {
        const secondPower = x => x * x;  return secondPower(a) + secondPower(b);
        }
        
        a2plusb2(2, 3); // 4 + 9 = 13
        
        secondPower(3); // Anda tidak bisa melakukan ini!
    ```
- Event dalam javascript 
    Event adalah sesuatu yang terjadi pada element, misalnya memiliki sebuah tombol dihalaman website atau aplikasi yang kita bangun, dan kita ingin memberikan suatu aksi jika tombol tersebut di klik. jadi yang menjadi event tersebut adalah "KLIK".<br>
    Adapun macam-macam event dalam javascript :
    - onclick adalah event yang jika sebuah element html diklik.
    - onchange adalah event jika sebuah html berubah.
    - onmouseover adalah event jika sebuah element html diletakkan cursor mouse.
    - onmouseout adalah event jika saat cursor mouse meninggalkan element html.
    - onkeydown adalah event jika saat terjadi pengetikan pada element html.
    - onload adalah event ketika jika suatu element atau halaman dibuka.
    
    Contoh penggunaan event:<br>
    ```
    <!DOCTYPE html>
    <html>
    <head>
	    <title>Contoh Event</title>
    </head>
    <body>
	<h1>Mengenal Event Pada Javascript</h1>
	
	<!-- memberikan event pada element tombol -->
	<button onclick="tampilkan_nama()">KLIK SAYA</button>
 
	<!-- id hasil -->
	<div id="hasil"></div>
 
	<script>		
		// membuat function tampilkan_nama
		function tampilkan_nama(){
			document.getElementById("hasil").innerHTML = "<h3>Nama Saya Adalah Andi</h3>";
		}
		
	</script>
    </body>
    </html>
    ```
    
- Memanipulasi DOM<br>
    DOM(Document Object Model) adalah dokument(html) yang dimodelkan dalam sebuah object. Objek dari dokumen ini menyediakan sekumpulan fungsi dan atribut/data yang bisa kita manfaatkan dalam membuat program Javascript. Inilah yang disebut API (Application Programming Interface), DOM tidak hanya untuk dokumen HTML saja. DOM juga bisa digunakan untuk dokumen XML dan SVG.
    Terdapat beberapa fungsi yang bisa digunakan: <br>
    - getElementById() fungsi untuk memilih elemen berdasarkan atribut id.
    - getElementByName() fungsi untuk memilih elemen berdasarkan atribut name.
    - getElementByClassName() fungsi untuk memilih elemen berdasarkan atribut class.
    - getElementByTagName() fungsi untuk memilih elemen berdasarkan nama tag.
    - getElementByTagNameNS() fungsi untuk memilih elemen berdasarkan nama tag.
    - querySelector() fungsi untuk memilih elemen berdasarkan query.
    - querySelectorAll() fungsi untuk memilih elemen berdasarkan query.
    - dan lain-lain. <br>
    contoh penggunaan DOM :

    ```
    <!DOCTYPE html>
    <html>
    <head>
        <title>Memilih Elemen Berdasarkan ID</title>
    </head>
    <body>

    <!-- Elemen div yang akan kita pilih dari JS -->
    <div id="tutorial"></div>


    <script type="text/javascript">
        // mengakses elemen tutorial
        var tutorial = document.getElementById("tutorial");

        // mengisi teks ke dalam elemen
        tutorial.innerText = "Tutorial Javascript";

        // memberikan CSS ke elemen
        tutorial.style.backgroundColor = "gold";
        tutorial.style.padding = "10px";

    </script>

    </body>
    </html>
    ```
- Dynamic Typing adalah dimana tipe data bisa berubah2 atau dinamis dalam variabel.
cara melihat tipedata dengan operator typeof();

Referensi : <br>
https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/What_is_JavaScript
https://www.petanikode.com/
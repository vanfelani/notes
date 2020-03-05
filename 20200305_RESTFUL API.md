## RESTful API

REST (Representional State Transfer) adalah suatu arsitektur metode komunikasi yang menggunakan protokol HTTP untuk pertukaran data dan metode ini sering diterapkan dalam pengembangan aplikasi. Dimana tujuannya adalah untuk menjadikan sistem yang memiliki performa yang baik, cepat dan mudah untuk di kembangkan (scale) terutama dalam pertukaran dan komunikasi data. — *Developer Kudo*


Nah, itu kata Developer Kudo tentang REST. Lalu ada bedanya ga sih REST sama RESTful API?.

Okee, jadi gini bang. REST ( Representational State Transfer) itu arsitektur sebuah software, sedangkan RESTful API itu merupakan salah satu model implementasi dari web service. RESTful API merupakan implementasi dari API. RESTful itu protokol/aturan untuk melakukan REST. Jadi RESTful itu udah pasti REST, namun REST belum tentu bisa disebut RESTful.


**API itu apasih?**
API adalah singkatan dari Application Programming Interface. Merupakan suatu “penghubung” yang memungkinkan suatu aplikasi untuk berinteraksi dengan aplikasi lainnya dan berbagi data (https://en.wikipedia.org/wiki/Application_programming_interface).

**Output API**
Output dari RESTful ada XML dan JSON.

###### JSON (JavaScript Object Notation), beberapa ciri-ciri JSON.

1. Mudah di urai, bahkan oleh javascript pada sisi client, hanya object biasa
2. Data transport lebih kecil
3. Proses urai lebih cepat
   
###### XML (Extensible Markup Language), beberapa ciri-ciri XML

1. Butuh XML Document untuk mengurai seperti Xpath
2. Data transport lebih besar
3. Proses urai lebih lambat
>Sumber : http://slides.com/ferrisutanto/mengenal-restful-api#/20


### REST Resource Naming Guide   

Dalam REST, representasi data primer disebut Resource. Resource sendiri adalah penamaan resource REST yang kuat dan konsisten.

**FITUR - FITUR DALAM RESOURCE**

Dalam penamaan Resource biasanya menggunakan kata benda. Untuk penjelasan lebih lanjut, mari kita membagi *resource archetypes* menjadi empat kategori (document, collection, store and controller). Keempat Reource ini sebagai Default penamaan dalam REST.

1. Document
   Document adalah konsep tunggal yang mirip dengan contoh objek atau catatan database.
   >Contohnya: http://api.tutorial.rest.org

2. Collection
   Collection Reource adalah kumpulan Resource yang dikelola server. Klien juga dapat menambahkan Resource baru.
   > Contohnya: http: //.../blog/posts

3. Strore
   Strore sendiri adalah repositori Resource yang dikelola klien. Resource *Store* memungkinkan klien memasukkan Resource, mengeluarkannya, dan memutuskan kapan harus menghapusnya. Di *Store* mereka sendiri tidak membuat Resource baru. Sebaliknya setiap Resource yang disimpan memiliki URL yang dipilih oleh klien saat awalnya dimasukkan ke *Store*.
   >Contohnya: PUT / posting / 1234

4. Control
   Contoh berfungsi sebagai pengontrol membuat model konsep prosedural yang dapat dieksekusi, dengan input dan mendapatkan nilai kembali.


### Hypertext Tranfer Protocol (HTTP)
HTTP adalah protocol yang stateles, karna setiap perintah dieksekusi secara independen. tanpa sepengetahuan comand yang dieksekusi sebelumnya. Fungsinya sendiri untuk berkomunikasi dengan protokol http. 

HTTP sendiri mempunyai standar error (status error codenya). dia punya status code yang sudah di definisikan.
Contohnya: 

**HTTP STATUS CODE**
| KATEGORI  | DESKRIPSI |
| ----- | --- |
| 1xx: Informasi   | Mengkomunikasikan informasi tingkat protokol transfer.  |
| 2xx: Sukses | Menunjukkan bahwa permintaan klien diterima dengan sukses.  |
| 3xx: Pengalihan/Redirection | Menunjukkan bahwa klien harus mengambil beberapa tindakan tambahan untuk menyelesaikan permintaan mereka.  |
| 4xx: Client Error | Kategori kode status kesalahan ini mengarahkan jari ke klien.  |
| 5xx: Server Error | Server bertanggung jawab atas kode status kesalahan ini.  |

Status code isinya 3 Angka.
Contohnya:

+ 200 (OK)
+ 201 (Created)
+ 202 (Accepted)
+ 204 (No Content)
+ 301 (Moved Permanently)
+ 302 (Found)
+ DLL


Untuk Refresensi lengkapnya silahkan klik link dibawah!!
[Klik disini!!](https://restfulapi.net/http-status-codes/)

**HTTP request methods**

| NAMA METODE  | DESKRIPSI |
| ----- | --- |
| GET | untuk mengirimkan nilai (value) variabel ke file lain yang telah diatur oleh sang programmer.  |
| POST | untuk mengirimkan nilai (value) variabel ke file lain yang telah diatur oleh sang programmer.  |
| HEAD | Menunjukkan bahwa klien harus mengambil beberapa tindakan tambahan untuk menyelesaikan permintaan mereka.  |
| PUT | Kategori kode status kesalahan ini mengarahkan jari ke klien.  |
| CONNECT | Server bertanggung jawab atas kode status kesalahan ini.  |
| OPTIONS | Server bertanggung jawab atas kode status kesalahan ini.  |
| TRACE | Server bertanggung jawab atas kode status kesalahan ini.  |
| PATH | Server bertanggung jawab atas kode status kesalahan ini.  |

Note: Perbedaan POST dan GET
>Method POST akan mengirimkan data atau nilai langsung ke action untuk ditampung, tanpa menampilkan pada URL. Sedangkan method GET akan menampilkan data/nilai pada URL, kemudian akan ditampung oleh action.

##### METODE POST
![POST](https://www.dumetschool.com/images/fck/getpost3.jpg)

>>http://localhost:8080/Aditya
Metode POST bisa juga menampilkan parameternya, tetapi standarnya tidak ditampilkan dan akan ditampilkan di Body. 

##### METODE GET
![GET](https://www.dumetschool.com/images/fck/getpost4.jpg)

>http://localhost:8080/Aditya?name=didit&age=12

+ **?** memberikan parameter
+ **=** isi nya
+ **&** parameter berikutnya




>Referenses : spring.io
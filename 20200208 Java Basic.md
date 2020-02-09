
<h2>Return</h2>
<h3>Returning a Value from a Method (Mengembalikan Nilai dari Metode)</h3>
	Method yang mengembalikan nilai akan menghasilkan nilai ketika method ini dipanggil. Untuk mengembalikan nilai harus menggunakan keyword return.
	
	
## Contoh

```java
		static int luasPersegi(int sisi){
    			int luas = sisi * sisi;
    			return luas;
		}
```

<h3>Returning a Class or Interface (Mengembalikan Class )</h3>

Sekarang anggaplah Anda memiliki metode yang dinyatakan untuk mengembalikan Number:

```java
public Number returnANumber() {
    ...
}
```



<h2> This </h2>
menggunakan kata kunci this untuk mengisi variabel.
contoh :
```java
class User {
    private String username;
    private String password;

    // ini method setter
    public void setUsername(String username){
        this.username = username;
    }

    public void setPassword(String password){
        this.password = password;
    }

    // ini method getter
    public String getUsername(){
        return this.username;
    }

    public String getPassword(){
        return this.password;
    }
}
```
Perhatikan yang diatas! this kita gunakan di setiap method.
misalnya, jika this di hilangkan :

```java
class User {
    private String username;
    private String password;

    public void setUsername(String username){
        username = username;
    }
 }
```
Apa yang akan terjadi?

Yak! komputer akan bingung…

Karena tidak tahu variabel username yang mana yang dimaksud. Apakah variabel yang di class (private String username) ataukah variabel username yang ada di dalam parameter.
Apakah kita bisa menggunakan this di luar class?

Tidak, this hanya bisa digunakan di dalam class saja.


<h2>Controlling Access to Members of a Class </h2>

Secara umum ada 3 macam modifier yang digunakan dalam Java: public, private, dan protected.
Apabila kita tidak menggunakan tiga kata kunci tersebut, maka member atau class itu tidak menggunakan modifier (no modifier). Masing-masing modifier akan menentukan di mana saja member bisa diakses.


Berikut ini tabel jangkauan untuk masing-masing modifier:

| Modifier    | Class | Package  | Subclass  | World  |
| --------    | ----- | -------  | --------  | -----  |
| public      |	Y	  | Y        | Y         | 	Y     |
| protected   | Y     |	Y	     | Y         |	N     |
| no modifier |	Y     |	Y	     | N         |  N     |
| private	  | Y	  | N        | N         |  N     |

Keterangan:

>
Y artinya bisa diakses;
N artinya tidak bisa diakses;
Subclass artinya class anak;
World artinya seluruh package di aplikasi.

Pada tabel di atas… apabila kita tidak menggunakan modifier (no modifier), maka class dan member hanya akan bisa diakses dari Class itu sendiri dan package (class yang berada satu package dengannya).

Agar bisa diakses dari mana saja, maka kita harus memberikan modifier public.

Mari kita lihat contohnya…
#### 1. Public
Modifier public akan membuat member dan class bisa di akses dari mana saja.

Contoh:
```java
package modifier;

class Person {
    public String name;

    public changeName(String newName){
        this.name = newName;
    }
}
```
Pada class Preson terdapat dua member, yaitu:

 >1.atribut name
 2.method changeName()
 
Kedua member tersebut kita berikan modifier public. Artinya mereka akan bisa diakses dari mana saja. Namun, class Person tidak kita berikan modifier. Maka yang akan terjadi adalah class tersebut tidak akan bisa diimpor (diakses) dari luar package.

#### 2. Private
Modifier private akan membuat member hanya bisa diakses oleh dari dalam class itu sendiri.

Perlu diingat:

Modifier private tidak bisa diberikan kepada class, enum, dan interface. Modifier private hanya bisa diberikan kepada member class.

Contoh:
```java
class Person {
    private String name;

    public void setName(name){
        this.name = name;
    }

    public String getName(){
        return this.name;
    }
}
```
Pada contoh di atas, kita memberikan modifier private pada atribut name dan modifier public pada method setName() dan getName().

#### 3. Protected
Modifier protected akan membuat member dan class hanya bisa diakses dari:

>Class itu sendiri;
Sub class atau class anak;
Package (class yang berada satu package dengannya).

Modifier protected juga hanya boleh digunakan pada member saja.

Contoh:
```java
package modifier;

public class Person {
    protected String name;
    
    public void setName(String name){
        this.name = name;
    }
    
    public String getName(){
        return this.name;
    }
}
```
Pada contoh di atas, kita memberikan modifier protected pada atribut name.

Apabila kita coba mengakses dari class yang satu package dengannya, maka tidak akan terjadi error.

Namun, apabila kita mencoba mengakses dari luar package seperti ini:
```java
import modifier.Person;

public class Author {
    
    Person p = new Person();

    public Author() {
        // akan terjadi error di sini karena atribut name 
        // telah diberikan modifier protected
        p.name = "BOOTCAMP";
    }
}
```
Maka akan terjadi eror




## Understanding Class Members


### Class Variables
Ketika sejumlah objek dibuat dari cetak biru kelas yang sama, mereka masing-masing memiliki salinan variabel instance yang berbeda . Dalam kasus Bicyclekelas, variabel instance yang cadence, gear, dan speed. Setiap Bicycleobjek memiliki nilai sendiri untuk variabel-variabel ini, disimpan di lokasi memori yang berbeda.

Terkadang, Anda ingin memiliki variabel yang umum untuk semua objek. Ini dilakukan dengan staticpengubah. Bidang yang memiliki staticpengubah dalam deklarasi mereka disebut bidang statis atau variabel kelas . Mereka terkait dengan kelas, bukan dengan objek apa pun. Setiap instance kelas membagikan variabel kelas, yang berada di satu lokasi tetap dalam memori. Objek apa pun dapat mengubah nilai variabel kelas, tetapi variabel kelas juga dapat dimanipulasi tanpa membuat turunan kelas.

Misalnya, Anda ingin membuat sejumlah Bicycleobjek dan menetapkan masing-masing nomor seri, dimulai dengan 1 untuk objek pertama. Nomor ID ini unik untuk setiap objek dan karenanya merupakan variabel instan. Pada saat yang sama, Anda perlu bidang untuk melacak berapa banyak Bicycleobjek yang telah dibuat sehingga Anda tahu ID apa yang akan ditetapkan untuk yang berikutnya. Bidang seperti itu tidak terkait dengan objek individu, tetapi dengan kelas secara keseluruhan. Untuk ini, Anda memerlukan variabel kelas numberOfBicycles,, sebagai berikut:
```java
public class Bicycle {
        
    private int cadence;
    private int gear;
    private int speed;
        
   // tambahkan variabel instan untuk ID objek 
    private int id;
    
    // tambahkan variabel kelas untuk 
    // jumlah objek Sepeda instantiated 
    
    private static int numberOfBicycles = 0;
        ...
}

```
Variabel kelas direferensikan oleh nama kelas itu sendiri, seperti pada
```java
Bicycle.numberOfBicycles
```
Ini memperjelas bahwa mereka adalah variabel kelas.
Anda bisa menggunakan Bicyclekonstruktor untuk menyetel idvariabel instan dan menambahkan numberOfBicyclesvariabel kelas:
```java
public class Bicycle {
        
    private int cadence;
    private int gear;
    private int speed;
    private int id;
    private static int numberOfBicycles = 0;
        
    public Bicycle(int startCadence, int startSpeed, int startGear){
        gear = startGear;
        cadence = startCadence;
        speed = startSpeed;

        // peningkatan jumlah Sepeda 
        // dan menetapkan nomor ID 
        id = ++numberOfBicycles;
    }

    // metode baru untuk mengembalikan variabel instance instan ID 
    public int getID() {
        return id;
    }
        ...
}
```
### Class Methods
Bahasa pemrograman Java mendukung metode statis dan juga variabel statis. Metode statis, yang memiliki staticpengubah dalam deklarasi mereka, harus dipanggil dengan nama kelas, tanpa perlu membuat turunan dari kelas, seperti dalam
```java
ClassName.methodName (args)
```
Catatan:  Anda juga bisa merujuk ke metode statis dengan referensi objek seperti
```java
instanceName.methodName (args)
```
tetapi ini tidak dianjurkan karena tidak memperjelas bahwa mereka adalah metode kelas.
Penggunaan umum untuk metode statis adalah untuk mengakses bidang statis. Sebagai contoh, kita bisa menambahkan metode statis ke Bicyclekelas untuk mengakses numberOfBicyclesbidang statis:
```java
public static int getNumberOfBicycles () { 
    return numberOfBicycles; 
}
```
Tidak semua kombinasi instance dan variabel kelas dan metode diizinkan:

Metode instance dapat mengakses variabel instan dan metode instance secara langsung.
Metode instance dapat mengakses variabel kelas dan metode kelas secara langsung.
Metode kelas dapat mengakses variabel kelas dan metode kelas secara langsung.
Metode kelas tidak dapat mengakses variabel instan atau metode instan secara langsung — mereka harus menggunakan referensi objek. Juga, metode kelas tidak dapat menggunakan thiskata kunci karena tidak ada contoh untuk thismerujuk.



## Initializing Fields
#### Static Initialization Blocks
Sebuah blok statis inisialisasi adalah blok normal kode diapit oleh kurung, { }dan didahului oleh statickata kunci. Berikut ini sebuah contoh:
```java
static { 
    // kode apa pun yang diperlukan untuk inisialisasi ada di sini 
}
```
Kelas dapat memiliki sejumlah blok inisialisasi statis, dan mereka dapat muncul di mana saja di tubuh kelas. Sistem runtime menjamin bahwa blok inisialisasi statis dipanggil dalam urutan yang muncul dalam kode sumber.

Ada alternatif untuk blok statis - Anda dapat menulis metode statis pribadi:
```java
class Whatever {
    public static varType myVar = initializeClassVariable();
        
    private static varType initializeClassVariable() {

        // initialization code goes here
    }
}
```

Keuntungan dari metode statis privat adalah bahwa mereka dapat digunakan kembali nanti jika Anda perlu menginisialisasi ulang variabel kelas.
#### Initializing Instance Members
Biasanya, Anda akan meletakkan kode untuk menginisialisasi variabel instan dalam konstruktor. Ada dua alternatif untuk menggunakan konstruktor untuk menginisialisasi variabel contoh: blok penginisialisasi dan metode akhir.

Blok inisialisasi untuk variabel contoh terlihat seperti blok inisialisasi statis, tetapi tanpa statickata kunci:
```java
{ 
    // kode apa saja yang diperlukan untuk inisialisasi ada di sini 
}
```
Kompilator Java menyalin blok penginisialisasi ke setiap konstruktor. Oleh karena itu, pendekatan ini dapat digunakan untuk berbagi blok kode antara beberapa konstruktor.

Sebuah metode akhir tidak bisa ditimpa dalam subclass. Ini dibahas dalam pelajaran tentang antarmuka dan warisan. Berikut adalah contoh penggunaan metode final untuk menginisialisasi variabel instan:

```java
class Whatever {
    private varType myVar = initializeInstanceVariable();
        
    protected final varType initializeInstanceVariable() {

        // kode inisialisasi ada di sini 
    }
}
```
Ini sangat berguna jika subclass mungkin ingin menggunakan kembali metode inisialisasi. Metode ini final karena memanggil metode non-final selama inisialisasi instance dapat menyebabkan masalah.


## Nested Classes
Bahasa pemrograman Java memungkinkan Anda untuk mendefinisikan kelas dalam kelas lain. Kelas semacam itu disebut kelas bersarang dan diilustrasikan di sini:
```java
class OuterClass { 
    ... 
    class NestedClass { 
        ... 
    } 
}
```

 bersarang dibagi menjadi dua kategori: 
> statis dan non-statis. Kelas bersarang yang dideklarasikan static disebut kelas bersarang statis .
 Kelas bersarang non-statis disebut kelas dalam .
 
Kelas bersarang adalah anggota kelas terlampir. Kelas bersarang non-statis (kelas dalam) memiliki akses ke anggota lain dari kelas terlampir, bahkan jika mereka dinyatakan pribadi. Kelas bersarang statis tidak memiliki akses ke anggota lain dari kelas terlampir. Sebagai anggota dari OuterClass, kelas bersarang dapat dinyatakan private, public, protected, atau paket swasta . (Ingat bahwa kelas luar hanya dapat dideklarasikan publicatau dipaketkan untuk pribadi .)

#### Alasan kuat untuk menggunakan kelas bersarang meliputi yang berikut:
>Ini adalah cara pengelompokan kelas secara logis yang hanya digunakan di satu tempat : Jika kelas hanya berguna untuk satu kelas lain, maka logis untuk menanamkannya di kelas itu dan menjaga keduanya bersama-sama. Menempatkan "kelas pembantu" seperti itu membuat paket mereka lebih efisien.

>Ini meningkatkan enkapsulasi : Pertimbangkan dua kelas tingkat atas, A dan B, di mana B membutuhkan akses ke anggota A yang seharusnya dinyatakan private. Dengan menyembunyikan kelas B dalam kelas A, anggota A dapat dinyatakan pribadi dan B dapat mengaksesnya. Selain itu, B sendiri dapat disembunyikan dari dunia luar.

>Ini dapat menyebabkan kode lebih mudah dibaca dan dipelihara : Bersarang kelas kecil dalam kelas tingkat atas menempatkan kode lebih dekat ke tempat kode itu digunakan.


#### inner Class non-static

Inner Class adalah class yang tidak berada pada top level atau class yang dideklarasikan didalam class lain(Outer class). untuk mengakses variable atau method pada class luar, kita perlu membuat Instance/Objek Class Luar didalam Inner Class.

 

Innerclass memerlukan sebuah Instance/Objek dari ClassLuar untuk mengakses secara langsung mathod atau variablenya, kemuadian kita Instance Inner Classnya. Source codenya seperti berikut ini:
```java
package BOOTCAMP;

//Outer Class/Kelas Luar
public class KelasLuar {
    
    //Class dalam/Inner Class Pertama
    private class Mobil{
        private String merk = "SUZUKI";
        private float kecepatan = 360.0f;
        private void jalankan(){
            System.out.println("Merk Mobil: "+merk);
            System.out.println("Kecepatan Mobil: "+kecepatan);
        }
    }
    
    //Class dalam/Inner Class Kedua
    private class Pengguna{
        private String nama = "Wildan";
        private int umur = 19;
        private void identitas(){
            System.out.println("Nama Saya: "+nama);
            System.out.println("Usia Saya: "+umur);
        }
    }
    
    public static void main(String[] args){
        //Membuat Instance dari KelasLuar
        KelasLuar outerclass = new KelasLuar();
        //Membuat Instance dari KelasDalam (Mobil)
        KelasLuar.Mobil data1 = outerclass.new Mobil();
        //Membuat Instance dari KelasDalam (Pengguna)
        KelasLuar.Pengguna data2 = outerclass.new Pengguna();
        
        //Menampilkan Hasil Output
        System.out.println("===== DATA DARI CLASS MOBIL ========");
        data1.jalankan();
        System.out.println("===== DATA DARI CLASS PENGGUNA =====");
        data2.identitas();
    }
}
```


Penggunaan Inner Class non-static pada Java Inner Class dapat digunakan untuk mengelompokan sesutu, jika kita mempunyai beberapa class yang mimiliki fungsi yang berbeda.

#### Inner Class static

Untuk mengubah Inner Class menjadi static, kita hanya perlu menambahkan kata kunci static di belakang class, Yang membedakan class static dengan non-static adalah pada class static kita tidak perlu Menginstance/Membuat objek dari classLuar terlebih dahulu, Inner Class static hanya perlu membuat instance dari classDalamnya saja.

Inner Class static lebih mudah dan praktis digunakan dibandingkan dengan non-static. Contoh sederhananya seperti berikut ini:
```java
package BOOTCAMP;

//Outer Class/Kelas Luar
public class KelasLuar {
    
    //Class dalam/Inner Class Static
    private static class Programming{
        private String language;
        private void setLanguage(String language){
            this.language = language;
        }
        private String getLanguage(){
            return language;
        }
    }
    
    public static void main(String[] args){
        //Membuat Instance dari Kelas Dalam (Programming)
        KelasLuar.Programming MyLanguage = new KelasLuar.Programming();
        
        //Memasukan Nilai/Value
        MyLanguage.setLanguage("Java");
        
        //Menampilkan Hasil Output
        System.out.println("Saya Sedang Mempelajari: "+MyLanguage.getLanguage());
    }
}
```


Penggunaan Inner Class static pada Java

>ada dua jenis class tambahan dalam inner class, Anda bisa mendeklarasikan kelas dalam di dalam tubuh metode. Kelas-kelas ini dikenal sebagai **local class** . Anda juga bisa mendeklarasikan kelas dalam di dalam tubuh metode tanpa menyebutkan kelas. Kelas-kelas ini dikenal sebagai **anonymus class.**

#### *Local Classes
Kelas lokal adalah kelas yang didefinisikan dalam sebuah blok , yang merupakan kelompok pernyataan nol atau lebih antara kawat gigi seimbang. Anda biasanya menemukan kelas-kelas lokal yang didefinisikan dalam tubuh metode.

```java
public class LocalClassExample {
  
    static String regularExpression = "[^0-9]";
  
    public static void validatePhoneNumber(
        String phoneNumber1, String phoneNumber2) {
      
        final int numberLength = 10;
        
        // Valid in JDK 8 and later:
       
        // int numberLength = 10;
       
        class PhoneNumber {
            
            String formattedPhoneNumber = null;

            PhoneNumber(String phoneNumber){
                // numberLength = 7;
                String currentNumber = phoneNumber.replaceAll(
                  regularExpression, "");
                if (currentNumber.length() == numberLength)
                    formattedPhoneNumber = currentNumber;
                else
                    formattedPhoneNumber = null;
            }

            public String getNumber() {
                return formattedPhoneNumber;
            }
            
          
        }

        PhoneNumber myNumber1 = new PhoneNumber(phoneNumber1);
        PhoneNumber myNumber2 = new PhoneNumber(phoneNumber2);
        
        // Valid in JDK 8 and later:

//        myNumber1.printOriginalNumbers();

        if (myNumber1.getNumber() == null) 
            System.out.println("First number is invalid");
        else
            System.out.println("First number is " + myNumber1.getNumber());
        if (myNumber2.getNumber() == null)
            System.out.println("Second number is invalid");
        else
            System.out.println("Second number is " + myNumber2.getNumber());

    }

    public static void main(String... args) {
        validatePhoneNumber("123-456-7890", "456-7890");
    }
}
```

#### *Anonymous class
Apa itu Class Anonymous?
Class Anonymous adalah class yang tidak memiliki nama. Biasanya dibuat hanya untuk sekali pakai saja. Pada dasarnya class anonymous sama seperti class biasa. 

Yang membedakan adalah tujuan ia dibuat.

Biasanya class anonymous dibuat untuk mengimplementasikan interface dan class abstrak secara langsung.

Mengapa Harus Menggunakan Class Anonymous?

Anonymous class biasanya kita butuhkan saat tidak ingin membuat implementasi dari interface dan class abstrak dalam file Java yang berbeda.

Kita ingin.. implementasinya langsung di dalam kode yang sedang ditulis.

Misalnya gini:

(kita pakai contoh kasus)

Kita mau pakai sebuah tombol dan tombol tersebut punya interfece bernama Clickable yang akan meng-handle bagaimana tombol itu diklik.
```java
// ini interface yang akan menangani klik pada tombol
interface Clickable {
  void onClick();
  void onHover();
}


// dan ini class Tombol
class Button {
  void setClickAction(Clickable event){
    event.onClick();
  }
}
```
Biasanya kita akan melakukan implementasi seperti ini:
```java
class SubmitPost implements Clickable {
  // kode implementasi di sini
}
```
Lalu membuat objek tombol pada main method:
```java
Button btn = new Button();
Clickable submitAction = new SubmitPost();
btn.setClickAction(submitAction);
```
Nah ini sebenarnya bisa kita buat lebih sederhana dengan Class Anonymous.
```java
Button btn = new Button();
Clickable submitAction = new SubmitPost();

// menggunakan class anonymous untuk implementasi interface
btn.setClickAction(new Clickable(){
  // kode implementasi di sini
});
```
Jadinya kita tidak perlu lagi membuat class SubmitPost atau implementasi dari interface Clickable, karena sudah dibuat dengan class anonymous.

Sudah paham kan mengapa harus pakai class anonymous?

**Akses Variabel di Anonymous Class**
Salah satu keuntungan saat kita menggunakan anonymous class adalah bisa mengakses variabel yang ada di dalam class tempat class anonymous itu dibaut.

Contoh, sekarang coba ubah kode yang ada di class Main menjadi seperti ini:
```java
public class Main {
    
    // membuat variabel di dalam class
    static String title = "Tutorial Anonymous Class";

    public static void main(String[] args) {
        
        // membuat variabel di dalam method main
        String name = "Bootcamp";
        
        Button btn = new Button();
        
        // membuat class anonymous untuk implemen interface
        btn.setClickAction(new Clickable() {
            // membuat variabel di dalam class anonymous
            String message = "belajar Anonymous Class di Java";
            
            
            public void onClick() {
                System.out.println("Tombol sudah diklik!");
                System.out.println("Yay!");
                // mengakses variabel
                System.out.println("Hello " + name);
                System.out.println(title);
                System.out.println(message);
            }

        });
        
        // mencoba klik tombol
        btn.doClick();
        
    }
}
```
***Access local variabel berdasarkan scope class yang ditempatinya dan access member dari anonymous class***
Seperti halnya local class, anonymous class juga dapat capture variabel. Class ini memiliki kesamaan dalam hal access local variabel berdasarkan scope dari class yang ditempatinya, seperti :

>Anonymous class dapat mengakses member dari class yang ditempatinya
Anonymous class tidak dapat mengakses local variabel dari scope class yang ditempatinya apabila local variabel tersebut tidak dideklarsikan final atau effectively final
Seperti nested class, dalam deklarasi tipe(variabel) dalam anonymous class dapa sama(shadow) dengan pendeklarasian variabel dalam scope class yang ditempatinya. Untuk artikel shadowing silahkan baca disini.

**Anonymous juga memiliki point-point yang tidak di perbolehkan untuk dilakukan, seperti :**

>Kita tidak dapat mendeklarasikan static initializer atau member interface dalam anonymous class
Kita dapat mendeklarasikan static member dalam anonymous class apabila dideklarasikan sebagai constant variabel.

**Kita juga dapat mendeklarasikan beberapa point dalam anonymous class, seperti :**

>fields
extra method
instance initializer
local class
Terpenting, kita tidak dapat mendeklarasikan constructor dalam anonymous clas




<h2>Inheritance</h2>
    Merupakan konsep pemrograman diamana sebuah class dapat 'menurunkan' property dan method yang dimiliknya kepada class lain. Konsep inheritance digunakan untuk memanfaatkan fitur 'code reuse' untuk menghindari duplikasi kode program. Konsep inheritance membuat sebuah struktur atau 'hierachy' class dalam kode program. Class yang akan 'diturunkan' bisa disebut sebagai class induk (parent class), super class. Sedangkan class yang 'menerima penurunan' bisa disbut sebagai class anak (child class), sub class, derived class atau heir class.


<h3>Contoh Inheritance</h3>

> File: inheritance/BangunDatar.java

```java

package inheritance;

public class BangunDatar {
    
    float luas(){
        System.out.println("Menghitung laus bangun datar");
        return 0;
    }
    
    float keliling(){
        System.out.println("Menghitung keliling bangun datar");
        return 0;
    }
    
}

```
> File: inheritance/Persegi.java

``` java

package inheritance;

public class Persegi extends BangunDatar {
    float sisi;   
}

```
> File: inheritance/Lingkaran.java

``` java

package inheritance;

public class Lingkaran extends BangunDatar{
    
    // jari-jari lingkaran
    float r;
    
}

```
> File: inheritance/PersegiPanjang.java

``` java

package inheritance;

public class PersegiPanjang extends BangunDatar {
    float panjang;
    float lebar;
}

```
> File: inheritance/Segitiga.java

``` java

package inheritance;

public class Segitiga extends BangunDatar {
    
    float alas;
    float tinggi;
    
}

```

> File: inheritance/Main.java

``` java

package inheritance;

public class Main {
    public static void main(String[] args) {
        
        // membuat objek bangun datar
        BangunDatar bangunDatar = new BangunDatar();
        
        // membuat objek persegi dan mengisi nilai properti
        Persegi persegi = new Persegi();
        persegi.sisi = 2;
        
        // membuat objek Lingkaran dan mengisi nilai properti
        Lingkaran lingkaran = new Lingkaran();
        lingkaran.r = 22;
        
        // membuat objek Persegi Panjang dan mengisi nilai properti
        PersegiPanjang persegiPanjang = new PersegiPanjang();
        persegiPanjang.panjang = 8;
        persegiPanjang.lebar = 4;
        
        // membuat objek Segitiga dan mengisi nilai properti
        Segitiga mSegitiga = new Segitiga();
        mSegitiga.alas = 12;
        mSegitiga.tinggi = 8;
        
        
        // memanggil method luas dan keliling
        bangunDatar.luas();
        bangunDatar.keliling();
        
        persegi.luas();
        persegi.keliling();
        
        lingkaran.luas();
        lingkaran.keliling();
        
        persegiPanjang.luas();
        persegiPanjang.keliling();
        
        mSegitiga.luas();
        mSegitiga.keliling();
    }
}

<h3>Overriding method</h3>

Method Overriding dilakukan saat kita ingin membuat ulang sebuah method pada sub-class atau class anak. Method Overriding dapat dibuat dengan menambahkan anotasi @Override di atas nama method atau sebelum pembuatan method.

> Contoh Overriding method

``` java

class Persegi extends BangunDatar {
    float sisi;

    @Override
    float luas(){
        float luas = sisi * sisi;
        System.out.println("Luas Persegi: " + luas);
        return luas;
    }

    @Override
    float keliling(){
        float keliling = 4 * sisi;
        System.out.println("Keliling Persegi: " + keliling);
        return keliling;
    }
}

```
Artinya kita menulis ulang method luas() dan keliling() di class anak.

> File: Lingkaran.java

``` java 

package inheritance;

public class Lingkaran extends BangunDatar{
    
    // jari-jari lingkaran
    float r;
    
    @Override
    float luas(){
        float luas = (float) (Math.PI * r * r);
        System.out.println("Luas lingkaran: " + luas);
        return luas;
    }
    
    @Override
    float keliling(){
        float keliling = (float) (2 * Math.PI * r);
        System.out.println("Keliling Lingkaran: " + keliling);
        return keliling;
    }
    
}

```
Dalam rumus luas dan keliling lingkaran, kita bisa memanfaatkan konstanta Math.PI sebagai nilai PI. Konstanta ini sudah ada di Java.

> File: PersegiPanjang.Java

``` java

package inheritance;

public class PersegiPanjang extends BangunDatar {
    float panjang;
    float lebar;
    
    @Override
    float luas(){
        float luas = panjang * lebar;
        System.out.println("Luas Persegi Panjang:" + luas);
        return luas;
    }
    
    @Override
    float keliling(){
        float kll = 2*panjang + 2*lebar;
        System.out.println("Keliling Persegi Panjang: " + kll);
        return kll;
    }
}

```

> File: Segitiga.java

``` java

package inheritance;

public class Segitiga extends BangunDatar {
    
    float alas; 
    float tinggi;

    @Override
    float luas() {
        float luas = 1/2 * (alas * tinggi);
        System.out.println("Luas Segitiga: " + luas);
        return luas;
    }   
    
}

```

Untuk class Segitiga, kita hanya melakukan override terhadap method luas() saja. Karena untuk method keliling(), segitiga memiliki rumus yang berbeda-beda.

<h3>Hiding Method</h3>

Yaitu jika ada variabel yang sama antara parent dan sub class maka variable pada sub class di hide dan mengikuti variable parent.

> Contoh hiding method

``` java

public class Hewan {
  public void testInstanceMethod(){
    System.out.println("Instance method di class Hewan");
  }
  public static void testClassMethod(){
    System.out.println("Static method di class Hewan");
  }
}

```
Kode program diatas artinya : Mendeklarasikan class Hewan yang berposisi sebagai superclass dan mendeklarasikan instance method dan *static method* di dalamnya. Setelah itu, kita buat class Kucing yang berposisi sebagai subclass dari Hewan, yang akan mengoverride kedua method yang telah dideklarasikan dalam superclass diatas, untuk kode program nya perhatikan berikut ini:

``` java

public class Kucing extends Hewan {
  public void testInstanceMethod(){
    System.out.println("Instance method di class Kucing");
  }
  public static void testClassMethod(){
    System.out.println("Static method di class Kucing");
  }
  public static void main(String[] args){
    Kucing k = new Kucing();
    Hewan h = k;
    Hewan.testClassMethod();
    h.testInstanceMethod();
  }
}

```
Kode program diatas artinya : Mendeklarasikan subclass Kucing yang extends superclass Hewan, dan mengoverride instance dan stataic method miliki superclassnya. Bila kode program diatas kita eksekusi keluaran yang dihasilkan seperti berikut ini

Static method di class Hewan Instance method di class Kucing melihat keluaran yang dihasilkan diatas, maka untuk versio hidden static method dapat memanggil satu buah method dari superclass dan untuk version override dapat memanggil satu buah instance method miliki subclass.

<h2>Overriding</h2>
Method overriding merupakan method yang parrent class yang ditulis kembali oleh subclass.

<h3>Contoh Overriding</h2>

``` java

public class Binatang {
    public void begerak(){
        System.out.println("Binatang bergerak sesuai kemampuannya");
    }
    public void berkembangBiak(){
        System.out.println("Binatang berkembang biak sesuai kemampuannya");
    }

}

```

``` java

public class Mamalia extends Binatang {
    //overriding method parent class
    public void begerak(){
        System.out.println("Mamalia bergerak sebagian besar dengan kakinya");
    }    
    public void berlari(){
        System.out.println("Sebagian Mamalia dapat berlari");
    }
}

```

``` java

public class PenggunaanOverriding {
    public static void main(String[] args) {
        // TODO Auto-generated method stub
        Binatang b = new Binatang();
        Mamalia m = new Mamalia();
        Binatang bm = new Mamalia();
        
        b.begerak();
        m.begerak();
        bm.begerak();
        bm.berkembangBiak();
    }
}

```

<h2>Polymorphism</h2>

Polimorfisme dalam OOP adalah sebuah prinsip di mana class dapat memiliki banyak “bentuk” method yang berbeda-beda meskipun namanya sama.
Bentuk di sini dapat kita artikan: isinya berbeda, parameternya berbeda, dan tipe datanya berbeda.

<h3>Contoh Polymorphism</h3>

>Buatlah class baru dengan BangunDatar

``` java

public class BangunDatar {
    float luas(){
        System.out.println("Menghitung luas bangun datar");
        return 0;
    }
    
    float keliling(){
        System.out.println("Menghitung keliling bangun datar");
        return 0;
    }
}

```
> Berikutnya buat class lagi dengan nama Persegi

``` java

public class Persegi extends BangunDatar{
    int sisi;
    
    public Persegi(int sisi) {
        this.sisi = sisi;
    }
    
    @Override
    public float luas() {
        return this.sisi * this.sisi;
    }
    
    @Override
    public float keliling(){
        return this.sisi * 4;
    }
}
Berikut

```

> Berikutnya buat class Segitiga

``` java

public class Segitiga extends BangunDatar{
   int alas;
   int tinggi;

    public Segitiga(int alas, int tinggi) {
        this.alas = alas;
        this.tinggi = tinggi;
    }
   
    
   @Override
   public float luas(){
       return this.alas * this.tinggi;
   }
}

```

> Berikutnya buat class Lingkaran

``` java

public class Lingkaran extends BangunDatar {
    int r;

    public Lingkaran(int r) {
        this.r = r;
    }
    
    @Override
    public float luas(){
        return (float) (Math.PI * r * r);
    }
    
    @Override
    public float keliling(){
        return (float) (2 * Math.PI * r);
    }
    
}

```

> Terakhir, buat class Main

``` java

public class Main {
    public static void main(String[] args) {
        
        BangunDatar bangunDatar = new BangunDatar();
        Persegi persegi = new Persegi(4);
        Segitiga segitiga = new Segitiga(6, 3);
        Lingkaran lingkaran = new Lingkaran(50);
        
        // memanggil method luas dan keliling
        bangunDatar.luas();
        bangunDatar.keliling();
        
        System.out.println("Luas persegi: " + persegi.luas());
        System.out.println("keliling persegi: " + persegi.keliling());
        System.out.println("Luas segitiga: " + segitiga.luas());
        System.out.println("Luas lingkaran: " + lingkaran.luas());
        System.out.println("keliling lingkaran: " + lingkaran.keliling());
    }
}

```

<h2>Hidding Fields</h2>

    Di dalam kelas, bidang yang memiliki nama yang sama dengan bidang dalam superclass menyembunyikan bidang superclass, bahkan jika tipenya berbeda. Di dalam subkelas, bidang dalam superclass tidak dapat dirujuk dengan nama sederhana. Sebagai gantinya, bidang tersebut harus diakses melalui super, yang dibahas di bagian selanjutnya.


<h2>Object as a Superclass</h2>

    Merupakan istilah yang merujuk pada class yang dijadikan acuan pewarisan/penurunan data. Oleh karena itu bersifat umum.

<h2>The clone() Method</h2>

Jika sebuah class atau superclass mengimplement interface Cloneable, kita dapat menggunakan method clone() untuk membuat copy object dari class yang ditempatinya, kita dapat menggunakan sintaks dasar seperti berikut ini:

```java

acloneableObject.clone();

```

Kode program diatas artinya: Sintaks dasar dalam menggunakan method clone(). Object yang mengimplementasi method tersebut ditujukan untuk mengecheck apakah object tersebut mengimplement interface Cloneable. Untuk dapat menggunakan atau mengimplementasikan method ini ke dalam sebuah object, kita dapat menggunakan sintak dasarnya, seperti berikut ini:

``` java

public Object clone() throws CloneNotSupportedException

```

Kode program diatas artinya: Sintaks dasar dari method clone() yang digunakan untuk membuat dan mengembalikan(return) object hasil copy(clone). Arti “copy” adalah mengambil object dari class.

<h2>The equals() Method</h2>

Method equals di Java digunakan untuk membandingkan(compare) dua object apakah memiliki persamaan atau tidak secara reference. Method ini akan mengembalikan nilai kembalian true apabila kedua object equal. Selain method equals, class object juga menyediakan operator(==) untuk mengetahui apakah dua object sama atau tidak. Perlu diperhatikan, untuk tipe data primitive menggunakan operator(==) diperbolehkan. Akan tetapi untuk tipe data reference tidak diperbolehkan. Untuk compare tipe data reference kita harus menggunakan method equals.

> Sintaks dasar The equals() Method

``` java

public boolean equals(Object obj)

```

<h2>The finalize() Method</h2>

merupakan method kelas Object yang akan dieksekusi saat garbace collection menghapus sebuah object yang sudah tidak digunakan/terpakai pada memori.

<h2>The getClass() Method</h2>

Di Java method ini digunakan untuk return class object, selain itu juga dapat digunakan untuk mendapatkan informasi mengenai class yang di ambil informasinya, seperti nama class menggunakan method getSimpleName(), nama superclass menggunakan method getSuperclass() dan nama interface yang mengimplements getInterfaces() bila kita gunakan secara bersamaan dengan method getClass tadi.

> Sintaks dasar The getClass() Method

```java

String name = key.getClass().getName();

```

<h2>The hashCode() Method</h2>

adalah nilai yang dimiliki oleh setiap object/instance yang digunakan sebagai 'identitas dari object tersebut'. Sederhananya, jika nilai hashcode dari 2 objects sama, bisa diartikan bahwa 2 object tersebut adalah object yg sama. Implementasi default dari class Object biasanya menggunakan alamat memory dr object tsb.

> Sintaks dasar The hashCode() Method

```java

public static void main(String [] args){
  
  String string1 = "Bahasa Java";
  String string2 = "Bahasa Java";
  String string3 = new String("Bahasa Java");
  
  /**
  Mengetahui nilai hash code masing-masing string
  */
  int hashString1 = string1.hashCode();
  int hashString2 = string2.hashCode();
  int hashString3 = string3.hashCode();
  
  /**
  Memeriksa jika string equal dengan method equals(), maka hash code-nya juga sama
  */ 
  boolean cek1 = string1.equals(string2) && string1.hashCode() == string2.hashCode();
  boolean cek2 = string1.equals(string3) && string1.hashCode() == string3.hashCode();
  
  /**
  Menampilkan hasil pengecekan
  */
  System.out.println("Hash code string1 adalah " + hashString1);
  System.out.println("Hash code string2 adalah " + hashString2);
  System.out.println("Hash code string3 adalah " + hashString3);
  
  System.out.println();
  
  System.out.println("Apakah string1 dan string 2 equal dan nilai hash code-nya sama? " + cek1);
  System.out.println("Apakah string1 dan string 3 equal dan nilai hash code-nya sama? " + cek2);
  
 }
}

```

output

<h2>The toString() Method</h2>
Method ini digunakan untuk mendapatkan objek String yang mewakili nilai dari Nomor Object. Jika method mengambil tipe data primitif sebagai argumen, maka objek String yang mewakili nilai tipe data primitif akan dikembalikan.
Jika metode mengambil dua argumen, maka representasi String dari argumen pertama pada radix ditentukan oleh argumen kedua yang akan dikembalikan.

> Sintaks dasar The toString() Method

``` java

public class Test{ 

   public static void main(String args[]){
      Integer x = 5;

      System.out.println(x.toString());  
      System.out.println(Integer.toString(12)); 
   }
}

```

<h2>Writing Final Classes and Methods</h2>

Class yang dideklarasikan dengan keyword final di Java disebut dengan final class. Kita dapat mendeklarasikan sebuah class dengan menambahkan keyword final apabila kita menginginkan atau beranggapan class tersebut sudah complete atau tidak digunakan oleh class lain.

> Contoh Writing Final Classes and Methods

``` java

package com.wordpress.bmadi.morefinalmethods;
public class Person {
  public final String getName(){
    return "person";
  }
}

```
Kode program diatas artinya : Mendeklarasikan superclass Person yang mengandung final method, yaitu getName. Kemudian kita buat subclass CheapPerson yang inherit dari superclass diatas.

``` java

public class CheapPerson extends Person {
  
  @Override
  public final String getName(){
    return "cheap person";
  }
  
  public static void main(String[] args){
    CheapPerson cPerson = new CheapPerson();
    System.out.println(cPerson.getName());
  }
}

```
Kode program diatas artinya : Mendeklarasikan subclass CheapPerson yang inherit dari superclass Person, dan mengoverride method getName yang dimiliki oleh superclassnya.

``` java


public class Person1 {
  public String getName(){
    return "person";
  }
}

```
Kode program diatas artinya : Mendeklarasikan superclass Person1 yang tidak mengandung final method. Kemudian kita buat subclass CheapPerson yang inherit dari superclass diatas.

``` java

public class CheapPerson1 extends Person1 {
  
  @Override
  public final String getName(){
    return "cheap person";
  }
  
  public static void main(String[] args){
    CheapPerson1 cPerson = new CheapPerson1();
    System.out.println(cPerson.getName());
  }
}

```

Kode program diatas artinya : Mendeklarasikan subclass CheapPerson yang inherit dari superclass Person, dan mengoverride method getName yang dimiliki oleh superclassnya.

<h2>Abstract Methods and Classes</h2>
Abstract method merupakan sebuah method yang dideklarasikan dengan menambahkan keyword abstract pada deklarasinya, dan tanpa ada implementasi dari method tersebut. Dalam arti, hanya pendeklarasian saja, tanpa tanda sepasang kurung kurawal.

``` java 

abstract void setName();
abstract void setMakanan();

```
Kode program diatas artinya : Mendeklarasikan abstract method dengan nama setName dan setMakanan.

<h2>Abstract Classes Compared to Interfaces</h2>
Sebuah kelas abstrak adalah kelas yang dinyatakan abstract-itu mungkin atau mungkin tidak termasuk metode abstrak. Kelas abstrak tidak bisa dipakai, tetapi mereka bisa subkelas. Sebuah metode abstrak adalah metode yang dideklarasikan tanpa implementasi (tanpa kawat gigi, dan diikuti oleh titik koma), seperti ini: kekosongan abstrak moveTo (deltaX ganda, deltaY ganda). Jika suatu kelas menyertakan metode abstrak, maka kelas itu sendiri harus dideklarasikan abstract.

``` java

public abstract class GraphicObject { 
   // menyatakan bidang 
   // mendeklarasikan metode nonabstrak 
   abstrak void draw (); 
}

```
Ketika kelas abstrak disubklasifikasikan, subkelas biasanya menyediakan implementasi untuk semua metode abstrak di kelas induknya. Namun, jika tidak, maka subkelas juga harus dideklarasikan abstract.

<h2>Numbers</h2>
Number adalah superclass untuk class numeric wrapper seperti BigInteger, BigDecimal,  Byte, Double, Float, Integer, Long, Short. Class tersebut memiliki method yang bisa dibilang umum.

<h2>Formatting Numeric Print Output</h2>
Untuk menampilkan angka dengan format-format khusus, berkaitan dengan nilai mata uang, maka pada umumnya hanya diperlukan dua digit angka dibelakang koma pada outputnya.

> Contoh syntak Number

``` java

public static void main (String args []){
 
    double saldo = 1786462.654;
    double sukuBunga = 0.017;
    double bunga = saldo * sukuBunga;
 
    System.out.printf("Bunga bank adalah Rp.%4.2f", bunga);
  }
 
}

```

<h2>Beyond Basic Arithmetic</h2>

Bahasa pemrograman Java mendukung aritmatika dasar dengan operator aritmatiknya: +, -, *, /, dan%. The Math kelas dalam java.langpaket menyediakan metode dan konstanta untuk melakukan perhitungan matematika yang lebih maju.etode di Mathkelas semuanya statis, jadi Anda memanggilnya langsung dari kelas.

``` java
cos(angle);

```

<h2>Random Numbers</h2>
Untuk membuat angka random, kita menggunakan class Random yang terdapat pada package java.util, atau melalui method static random dari class Math. Objek dari class Random dapat menghasilkan random untuk  boolean, byte, float, double, int, long dan nilai Gaussian , sementara Math method random hanya dapat menghasilkan nilai double dalam rentang 0.0 ≤ a < 1.0, dimana  a adalah nilai yang dikembalikan oleh method random.

> Contoh random

``` java

Random randomNumbers = new Random;

int randomValue = randomNumbers.nextInt();

public class AngkaRandom {
 
 public static void main( String args[] ){
 Random angkaRandom = new Random(); 
 
 int hasil; 
 
 for ( int counter = 1; counter <= 100; counter++ ){
  hasil = 1 + angkaRandom.nextInt( 9 );
  System.out.printf( "%d ", hasil ); 
  if ( counter % 10 == 0 )
   System.out.println();
  }
 
 }
 
}

```
<h2>Characters</h2>
 Bahasa pemrograman Java menyediakan kelas pembungkus yang "membungkus" chardalam suatu Characterobjek untuk tujuan ini. Objek tipe Characterberisi bidang tunggal, yang tipenya adalah char. Kelas Karakter ini juga menawarkan sejumlah metode kelas yang berguna (yaitu statis) untuk memanipulasi karakter.

 > Contoh program Characters

 ``` java

public class MetodaCharacter {
 
   // Metoda main
   public static void main(String[] args) {
 
      Character chr1 = new Character('b');
      System.out.println();
      System.out.println("Character chr1 = new Character(\'b\');");
 
      char ch1 = chr1.charValue();
      System.out.println("ch1 = " + ch1);
      char ch2 = Character.toUpperCase(ch1);
      System.out.println("ch2 = " + ch2);
 
      boolean bool1 = Character.isLowerCase(ch1);
      System.out.println("Character.isLowerCase(ch1) = " + bool1);
      boolean bool2 = Character.isUpperCase(ch2);
      System.out.println("Character.isUpperCase(ch2) = " + bool2);
 
      System.out.println("chr1.equals(ch1) = " + chr1.equals(ch1));
   }
}

 ```

 <h2>Strings</h2>

 tipe data untuk teks yang merupakan gabungan huruf, angka, whitespace (spasi), dan berbagai karakter. Fungsi ini digunakan untuk membuat identifier String/teks. String juga sering disebut sebagai “array of char”.

 >Contoh Strings

 ``` java

class LatihanString{
public static void main(String[] args) {
String str="Selamat Datang di Program Studi Ilmu Komputer";
System.out.println("Variabel Str : " + str);
    }
}

 ```

<h2>Concatenating Strings</h2>

Method ini menambahkan satu String ke akhir String lainnya. Method ini mengembalikan sebuah String dengan nilai String yang telah ditambahkan dalam method ini yang nantinya akan diletakkan pada akhir String yang digunakan untuk memanggil method ini.

> Contoh 

``` java

 public class Test {

   public static void main(String args[]) {
      String s = "Aku adalah String pertama";
      s = s.concat(" dan aku adalah String yang akan digabungkan");
      System.out.println(s);
   }
}

```
<h2>Converting Between Numbers and Strings</h2>

subclass dari class Number memiliki beberapa wrap primitive, seperti Byte, Integer, Double, Float, Long dan Short yang telah mengincludkan method valueOf. Method inilah yang nantinya akan kita gunakan untuk mengconver string menjadi object yang kita inginkan, dalam hal ini number.

> Contoh Program

``` java

public class DemoValueOf1 {
  public static void main(String[] args){
    if(args.length == 2){
      // Convert string ke number
      float a = (Float.valueOf(args[0])).floatValue();
      float b = (Float.valueOf(args[1])).floatValue();
      System.out.println("a + b = " + (a + b));
      System.out.println("a - b = " + (a - b));
      System.out.println("a * b = " + (a * b));
      System.out.println("a / b = " + (a / b));
      System.out.println("a % b = " + (a % b));
    }else {
      System.out.println("Program ini" +
                         " meminta dua argument untuk diinputkan.");
    }
  }
}

``` 

<h2>Comparing Strings and Portions of Strings</h2>

<h2>The StringBuilder Class</h2>
Digunakan untuk membuat objek string yang mutable sama seperti class StringBuffer. Namun perbedaan utamanya terletak pada sinkronisasasi, sehingga StringBuilder ini tidak thread safe karena tidak disinkronisasi.


```java
public static void main(String[] args) {
StringBuilder SB=new StringBuilder();
SB.append ("JAVA Course at a2fahmi.com");
System.out.println(SB);
SB.append ("Android course at a2fahmi.com");
System.out.println(SB);

}

}
```

<h2>stirng buffer</h2>

Merupakan sebuah class library yang digunakan untuk mengolah data dan juga nilai karakter, class tersebut terdapat didalam package (java.lang), StringBuffer secara konsep, memiliki kemiripan dengan tipe data String, yaitu untuk menampilkan karakter. Perbedaannya terletak pada beberapa fungsi serta objek dari class StringBuffer. Kita dapat menambahkan ataupun menghapus karakter didalamnya.

> Contoh: Menambah Nilai pada Objek StringBuffer

``` java

public class string_demo {
    public static void main(String[] args){
        //Mendefinisikan Objek Beserta Nilainya
        StringBuffer data = new StringBuffer("Belajar");
        
        //Menambahkan Beberapa Nilai/Karakter String
        data.append(" Pemrograman");
        data.append(" Java");
        data.append(" Bersama Wildan");
        
        //Menampilkan Output
        System.out.println(data);
    }
}

```





























<h2>Generic</h2><hr width="100%">
    cara Java dalam melakukan generalisasi terhadap tipe data tanpa mengurangi kemampuan Java dalam menjaga keamanan penggunaan tipe data.
    Definisi :
     Tipe data berparameter yang bersifat generic atau di kenali pada saat runtime. 
     Menambah stabilisasi pada kode
     Memperjelas sebuah tipe data  
     Membuat bugs di kenali di awal & dapat terdeteksi saat di compile 
     Array List , iterator , dan Linked List adalah contoh dari kelas generic 
     Nama type parameter biasanya satu huruf dan huruf besar. 
     Beberapa type parameter yang umum digunakan pada generic : 
        E - Element
        K – Key 
        N – Number
        T - Type 
        V – Value
     Hanya bisa menerima tipe data non primitif 
     Generic hanya dapat menggunakan Object.Sehingga tipe data primitif harus diubah ke bentuk classnya .Contoh: int menjadi Integer

Contoh :
```java
public class Koleksi<T> {
private T data;
public T getData() {
return data;
}
public void setData(T data) {
this.data = data;
}
}
```
Generic ditandai dengan tanda kurung siku ' < > '. Pada kode di atas berarti kita membuat generic dengan simbol T, sehingga T dianggap sebagai tipe data dalam lingkup class tersebut. Sewaktu class Koleksi dipakai, T diganti menjadi tipe data tertentu.

<h3>WildCards         :</h3> 
    -> Gunakan wildcard <?> sebagai argumen
    -> Collection <?> bermakna collection yang tidak diketahui tipe datanya
<h3>Bounded Wildcards :</h3>
    -> mengkhususkan tipe data yang tidak diketahui menjadi subtipe dari tipe data tertentu 
Contoh :

```java
static void printCollection(
    Collection<? extends Number> c){
        for(Object o :c)
        System.out.println(o);
    }
    public static void main (String[] args){
        Collection<string> cs=new Vector<string>();
        printCollection(cs); // Compile Error
        List<integer> li= New ArrayList<integer>(10);
        printCollection(li); //No Compile Error
    }
)
```

<h3> Raw Types :
Class bertipe generic masih bisa di-instantiasi (penciptaan objek) tanpa menggunakan argumen
<h3> Generic Method    :
Pada method generic, simbol hanya berlaku pada method itu saja dan tidak berlaku pada method lain dalam class
<h3> Interoperating with Legacy Code 
Using Legacy Code In Generic Code 
<h3>Erasure  :
Compiler bertanggungjawab untuk “memahami” generics pada saat kompilasi.
 Namun compiler juga bertanggungjawab untuk menghapus “pemahaman” mengenai class generic, hal ini disebut type erasure.
 Informasi tipe data pada generic dihapus dari bytecode setelah kompilasi.
 Jadi generic-nya tidak wujud lagi pada saat runtime
 Setelah kompilasi, semua saling berbagi class yang sama



<h2>Package<b></h2><hr width="100%">
pengelompokkan dan pengorganisasian kelas-kelas dan interface yang sekelompok menjadi suatu unit tunggal dalam library. Membuat dan menggunakan Package. Package juga mempengaruhi mekanisme hak akses ke kelas-kelas di dalamnya <br>
<h3>Fungsi Package<b><h2>
mengelompokkan file kelas yang terkait (karena jenisnya, fungsinya atau karena alasan lainnya) pada direktori yang sama, dimana di dalam setiap kelasnya terdapar directive (statement java dalam code yang digunakan untuk membuat
kelas) package yang mengacu pada direktori tersebut.<br> 

<h3>Membuat dan Menggunakan Package</h3>
1. Mendeklarasikan dan memberi nama package.
    • Package di tulis dengan <b>lowerCase</b> di awali dengan huruf kecil
    • Menggambarkan kelas-kelas yang dibungkusnya 
    • Harus unik (berbeda dengan nama package standard) package standard)
    • Merepresentasikan path dari package tersebut.

Package examplepackage;

2. Membuat struktur dan nama direktori yang sesuai dengan struktur dan nama package
3. Mengkompilasi kelas-kelas sesuai dengan packagenya masing dengan packagenya masing-masing.

Contoh package standard :

java.lang (berisi kelas-kelas fundamental yang sering digunakan).
java.awt dan javax.swing (berisi kelas-kelas untuk membangun aplikasi GUI)
java.io (berisi kelas-kelas untuk proses input output)

<h3>Struktur Direktori</h3>
Package dapat bersarang di package lain, sehingga dapat dibuat hirarki package.
• Bentuk umum pernyataan package multilevel :
package namaPackage1[.namaPackage2[.namaPackage3]];

<h3>Menggunakan Package</h3>
Kelas yang menggunakan berada dalam direktori(package) yang sama dengan kelas-kelas yang digunakan. Maka tidak diperlukan import.
Kelas yang menggunakan berada dalam direktori(package) yang berbeda  dengan kelas-kelas yang digunakan. Maka pada awal source code di kelas pengguna harus mencantumkan : kelas pengguna harus mencantumkan :
import namaPackage.NamaKelas; atau
import namaPackage. import namaPackage. ;

<h2>Exception</h2><hr width="100%">
Peristiwa yang terjadi ketika program menemui kesalahan pada saat instruksi program dijalankan.
Ada yang terjadi (Throw) dan Menangkap (Catch)
2 macam :
A try Statement : Untuk menangkap exception . Try harus menyediakan handler untuk exceptionnya 
Method yang menyebutkan bisa /mungkin dapat melemparkan exception 

<h3>Klasifikasi class-class Exception:</h3>
<b>1.System error</b>, Error class ini akan menjelaskan mengenai sistem error internal, meskipun hal ini jarang terjadi. Namun jika error ini terjadi maka tidak banyak yang bisa dilakukan selain memberitahu user dan menghentikan program dengan baik.

Beberapa subclass dari class Error adalah:
• AnnotationFormatError
• AssertionError
• AWTError
• CoderMalfunctionError
• FactoryConfigurationError
2<b>.Exceptions</b>, direpresentasikan dalam class Exception yang menggambarkan kesalahan yang disebabkan karena program anda sendiri dan oleh sebab eksternal. Namun, error ini dapat ditangkap dan ditangani oleh program anda.
Beberapa subclass dari class Exception diantaranya adalah:

• IOException,
• RuntimeException,
• TimeoutException
• UnsupportedLookAndFeelException
• XMLParseException

<h3>3.Runtime Exception</h3>, direpresentasikan pada class RuntimeException yang menjelaskan mengenai kesalahan pada pemrograman seperti kesalahan casting, mengakses array out-of-bounds, dan juga error numerik. Runtime exceptions ini pada umumnya dilontarkan oleh JVM. Beberapa subclass dari class RuntimeException  diantaranya adalah:
• ClassCastException
• EmptyStackException
• EventException
• IllegalArgumentException,
• IndexOutOfBoundsException
• NullPointerException

Contoh Exception Handling :
```java 
import java.io.FileWriter;
import java.io.PrintWriter;
import java.util.List;

public class Generic1 {
        private static final int SIZE = 10;
        private List<Integer> list;

        public void writeList() {
            PrintWriter out = null;
            try {
                System.out.println("Entered try statement");
                out = new PrintWriter(new FileWriter("OutFile.txt"));
                for (int i = 0; i < SIZE; i++) {
                    out.println("Value at: " + i + " = " + list.get(i));
                }
            }
            catch (Exception e){

            }
        }
        public static void main(String[] args) {
            Generic1 app=new Generic1();
            app.writeList();
        }

    }
}
```

<h3>The Try Block</h3> 
    Langkah pertama dalam membangun Exception Handler adalah melemparkan exception dengan try block. Secara umum, blok Try terlihat seperti berikut ini:

```java
private List<Integer> list;
private static final int SIZE = 10;

public void writeList() {
    PrintWriter out = null;
    try {
        System.out.println("Entered try statement");
        out = new PrintWriter(new FileWriter("OutFile.txt"));
        for (int i = 0; i < SIZE; i++) {
            out.println("Value at: " + i + " = " + list.get(i));
        }
    }
    catch and finally blocks  . . .
}
```
<h3>The Catch Block</h3>
Jika anda sudah melihat contoh try maka secara tidak langsung anda sudah memahami kegunaan dari keyword ini. Dalam java, keyword catch harus dipasangkan dengan try. Kegunaan keyword ini adalah menangkap kesalahan atau bug yang terjadi dalam block try. Setelah menangkap kesalahan yang terjadi maka developer dapat melakukan hal apapun pada block catch sesuai keinginan developer.

````java
try {

} catch (IndexOutOfBoundsException e) {
    System.err.println("IndexOutOfBoundsException: " + e.getMessage());
} catch (IOException e) {
    System.err.println("Caught IOException: " + e.getMessage());
}
```

<h3>The Finally Block<b3>
Keyword ini merupakan keyword yang menunjukan bahwa blockprogram tersebut akan selalu dieksekusi meskipun adanya kesalahan yang muncul atau pun tidak ada.

``` java
finally {
    if (out != null) { 
        System.out.println("Closing PrintWriter");
        out.close(); 
    } else { 
        System.out.println("PrintWriter not open");
    } 
} 
```
the Finally block adalah kunci untuk mencegah kebocoran resource. Saat menutup file atau memulihkan resource, tempatkan kode di blok akhirnya untuk memastikan bahwa resource selalu dipulihkan.













 




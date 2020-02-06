**JAVA BASIC**
======================================================================
Java adalah bahasa pemprograman tingkat tinggi, sedangkan bahasa tingkat rendahnya adalah asembly. Java sendiri dibuat oleh James gosting dan Henry McGliton

**Fitur didalam Java**

simpple
OOP
Distrubute
dinamic
robust
secure
dll


**Cara compile java di terminal dan command promt;**

1. Buat kode java di Text editor atau IDE



 	public class test{
 		public static void main(String [] adit){
 		System.out.println(“Kita sedang belajar java”);
 		}
 	}



2. Buka terminal jika anda pengguna linux dan buka commandpromt jika anda pengguna windows. Kemudian compile file kalian dengan sintaks javac namafile jika ada kesalahan dari koding nya maka file tidak akan running error. Jika koding berhasil maka ketikan java namafile maka koding akan running dan menampilkan hasilnya.

Dalam java ada args/argumen yaitu Nilai yang ditampung dari seluruh argumen yang dikirimkan kepada sebuah fungsi.

Public static void main adalah argumen. 'String[]args' adalah parameter dari argumen.		



**PENGENALAN VARIBEL DALAM JAVA**
---------------------------------------------------------------------------------
Variabel adalah tempat menyimpanan nilai sementara.
Hal yang perlu diketahui dalam pembuatan variabel di java adalah cara penulisannya.
Format nya seperti ini :
'
 	<tipe data> <nama variabel>
Contohnya
 	int index = 1;
'

Java bersifat case sentisitive karena dari itu statement *int a; dengan  int A;* itu berbeda.



**TIPE DATA**

**Berikut ini macam-macam tipe data pada Java:**
    * char: Tipe data karakter, contoh Z
    * int: angka atau bilangan bulat, contoh 29
    * float: bilangan desimal, contoh 2.1
    * double: bilangan desimal juga, tapi lebih besar kapasistanya, contoh 2.1
    * String: kumpulan dari karakter yang membentuk teks, contoh Hello World!
    * boolean: tipe data yang hanya bernilai true dan false
    
    
**Expressions, Statements**

Kita telah mempelajari apa itu variables dan operator, sekararang saatnya kamu belajar tentang expressions, statement and blocks. Operator bisa digunakan untuk membuat expresi dengan sebuah nilai.

Ekspresi adalah suatu cara penulisan untuk memberikan atau memasukkan nilai kedalam variabel. Ekspresi secara umum dalam computer statement dituliskan sebagai:

Variabel_Nilai

Ekspresi merupakan suatu proses yang bersifat sequential, yang artinya bahwa proses dilakukan dari baris paling atas sampai baris terakhir. Sebagai contoh bila dituliskan:

a=10
a=5

Maka artinya pada baris pertama a bernilai 10, dan pada baris kedua a bernilai 5, sehingga nilai 10 diganti dengan nilai 5. Sehingga hasilnya a bernilai 5.
Ekspresi bukan hanya seperti diatas, tetapi dapat juga merupakan penulisan suatu formula dengan melibatkan variabel-variabel yang sudah ada sebelumnya.

**STATEMENT**
-----------------------------------------------------------------
Statement membentuk unit eksekusi yang lengkap. Jenis ekpresi berikut ini dapat dibuat menjadi pernyataan dengan mengakhiri ekpresi dengan tanda titik koma(;).

**Array**
-------------------------------------------------------------------------
Array termasuk spesial. Array adalah objek yang digunakan untuk menampung nilai dengan jumlah yang tetap yang setipe. Panjang array itu tetap, bisa menampung satu atau banyak data dengan syarat nilai itu tetap. 
Contohnya :

'Array dengan panjang 0 .. 9
Index array selalu dimulai dengan nol.'

Setiap item didalam aray disebut elemen, dan setiap elemen diakses berdasarkan nomer indexnya 

Contoh Program array;


Package com.enigma.testing;
public class test{
	public static void main(String [] args){
 	int [] anArray = new int[10];  // membuat 10 ruang yang masing – masing 
					     elemennya bernilai nol
 	anARray[0] = 5;
 	System.out.println(anArray[0]);
	}
}



Contoh 2 ;
public class test{
	public static void main(String [] args){
 	int [] anArray = {
 		1 , 2 , 3 , 4 , 5
 	};
 	anARray[0] = 5;
 	System.out.println(anArray[0]);
	}
}


 	Contoh 3;
 	public class test{
	public static void main(String [] args){
 	int [] anArray = {
 		1 , 2 , 3 , 4 , 5
 	};
 	anARray[0] = 5;
 	System.out.println(anArray[0]);
	}
}


Contoh Array Multidimensi
**
class MultiDimArrayDemo {
    public static void main(String[] args) {
        String[][] names = {
            {"Mr. ", "Mrs. ", "Ms. "},
            {"Smith", "Jones"}
        };
        // Mr. Smith
        System.out.println(names[0][0] + names[1][0]);
        // Ms. Jones
        System.out.println(names[0][2] + names[1][1]);
    }
}
**


Ada Method dari java namanya Copy Array
Contoh ;

**
class ArrayCopyDemo {
    public static void main(String[] args) {
        char[] copyFrom = { 'd', 'e', 'c', 'a', 'f', 'f', 'e',
                            'i', 'n', 'a', 't', 'e', 'd' };
        char[] copyTo = new char[7];

        System.arraycopy(copyFrom, 2, copyTo, 0, 3);
        System.out.println(new String(copyTo));
    }
}
Outputnya ; CDE

**


**Assignment, Arithmetic**

**Operator Assignment pada Java**

Operator Assignment adalah sebuah operator yang disimbolkan dengan lambang sama dengan (=).
Operator yang identik dengan simbol sama dengan ini memiliki dua (2) buah operand.

Operand sebelah kiri berupa variabel, operand sebelah kanan berupa nilai literal atau 
variabel lainnya. Untuk arah operasi operator ini,  dari sebelah kanan ke kiri, 
artinya nilai sebelah kanan akan dicopy ke sebelah kiri. Setelah operasi sukses 
dilakukan nilai variabel di sebelah kiri akan sama dengan nilai operand disebelah kanan.



**Operator Aritmatika**

Operator aritmatika digunkan untuk ekspresi matematika seperti perkalian,pembagian,
penjumlahan dan pengurangan. Operator aritmatika tidak hanya digunakan untuk penjumlahan saja.
operator ini pun bisa digunakan sebagai fungsi lain.
Contohnya :

tanda + jika nilainya String bisa gunakan untuk menggabungkan statement.

Referensi tulisan :
Trainer Enigmacamp Bpk. Yussin R. Hidayat
 docs.oracle.com




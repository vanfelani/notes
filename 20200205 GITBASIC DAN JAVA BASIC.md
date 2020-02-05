20200205 GIT BASIC dan JAVA BASIC
=================================


**GIT BASIC**
---------

**Git** adalah salah satu tool yang sering digunakan dalam proyek pengembangan software. Git bahkan menjadi tool yang wajib dipahami oleh programmer, karena banyak digunakan di mana-mana.

Server GIT kalau diUser Interface (UI) konfigurasinya menggunakan username dan password. Kalau menggunakan command prompt melalui sertifikat. Contohnya menggunakan SSH

Jika kita menggunakan SSH Key, kita tidak perlu lagi mengisi username dan password.
SSH Key adalah metode alternatif untuk autentikasi ke Gitlab. SSH Key cukup kita buat satu kali dan bahkan bisa digunakan lagi di tempat lain seperti GIthub dan Bitbucket.

SSH Key sendiri ada 2 yaitu :
	- SSH Private yang tidak bisa dishare keserver GIT 
 	- SSH Public yang bisa dishare keserver git

Langkah 1 membuat SSH Key untuk Gitlab:

1. Buka Terminal jika anda menggunakan Linux, buka command prompt jika anda menggunakan Windows.
2. Generate sebuah kunci ED25519 SSH :
       'ssh-keygen -t ed25519 -C "email@example.com"'
3. Kemudian buat directory config

 	'touch config'

   Isi config dengan
 	'Host git.enigmacamp.com'
 	'HostName git.enigmacamp.com'
 	'User git'
 	'IdentityFIle ~/.ssh/git_enigma_ed25519'
4. lalu kopikan ssh public ke website git.enigma
 	
5. coba tes koneksi dengan mengetik
 	'ssh -T git@git.enigmacamp.com'


Langkah 2 Membuat Respository
1. Pembuatan repositori dapat dilakukan dengan perintah git init nama-directory. 

Contoh: 'git init folder1'

Perintah tersebut akan membuat direktori bernama folder1. Kalau direktorinya sudah ada, maka Git akan melakukan inisialisasi di dalam direktori tersebut.
Perintah git init akan membuat sebuah direktori bernama .git di dalam proyek kita. Direktori ini digunakan Git sebagai database untuk menyimpan perubahan yang kita lakukan.


**PERINTAH – PERINTAH GIT COMMANDS**
-------------------------------------


1.git config

git config untuk mengatur email dan username:

'git config --global user.email didit@email.com'
2. git init
Ini digunakan untuk membuat repository baru. git init [nama foldernya]
'git init [nama foldernya]'

3. git status
Perintah ini digunakan untuk melihat status dari git kita. 
'git status'

4. git add
Dalam git itu ada 3 area dalam proses pengerjaanya mengerjakan.
    1. Working area – area yang belum di add 
    2. Staging area – area yang sudah di add dan siap di commit 
    3. Repository area – area yang sudah di commit 
Misalnya kita membuat file baru dalam repository nah file baru tersebut akan masuk ke working area dahulu sebelum kita melakukan git add caranya dengan!

'git add [namafile]'

Jika kita ingin memindahkan semua yang ada di working area ke staging area kita bisa memasukan perintah

'git add .'
Titik akhir menandakan stagging area.

5.git commit
Untuk meyimpang ke repository dengan perintah!

'git commit -m "isi aja terserah"/'

8. git log
Untuk menampilkan daftar commit yang sudah dibuat perintahnya!

'git log'

**Perintah Git Untuk Gitlabs Enigma**
------------------------------------------

1.git clone
Ini digunakan biasanya untuk mengcopy projeck kita yang ada di githu. Perintahnya sebagai berikut
'git clone [url repository gitlabs nya]'

2.git push
Biasa digunakan untuk mengupdate project yang ada di gitlabs dari git. Untuk melakukan push bisa diawali dengan mengclone terlebih dahulu lalu jika project kita sudah diubah kita bisa mengubahnya juga di gitlabs dengan printah!

**Git push**

untuk push remote dari local ke server

'git push origin master'

3.git pull
Ini adalah kebalikan dari git push kalo push untuk mengupdate project kita yang ada digitlabs. Kalo git pull untuk mengupdate project kita yang ada di local yang sudah di clone. Perintahnya!

'Git pull'













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


Cara compile java di terminal dan command promt;

1. Buat koding java di text editor


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

Berikut ini macam-macam tipe data pada Java:
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

'a=10
a=5'

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


**Assignment, Arithmetic, and Unary Operators**
Operator Assignment pada Java

Operator Sama Dengan
No
Operator
Nama Operasi
contoh
1
+=
Penjumlahan
A += B sama dengan A=A+B
2
-=
Pengurangan
A -= B sama dengan A=A-B
3
*=
Perkalian
A *= B sama dengan A=A*B
4
/=
Pembagian
A /= B sama dengan A=A/B
4
%=
Modulus
A %= B sama dengan A=A%B


Operator Aritmatika 
No
Simbol
Nama Operator
Deskripsi
1
+
Penjumlahan
Menjumlahkan 2 buah operand
2
-
Pengurangan
Mengurangi suatu Operand dengan Operand yang lainnya
3
*
Perkalian
Melakukan Perkalian dari 2 buah Operand
4
/
Pembagian
Membagi suatu Operand dengan Operand lainnya
5
%
Modulus
Menghasilkan sisa bagi dari hasil pembagian



**Operator Unary**

No
Simbol
Nama Operator
Deskripsi
1
+
Positif
Menandakan suatu bilangan menjadi bernilai positif
2
-
Negatif
Menandakan suatu bilangan menjadi bernilai negatif
3
++
Increment
Menambah 1 nilai keatas pada suatu operand(variabel)
4
--
Decrement
Penurunan: mengurangi 1 nilai kebawah pada operand(variabel)


Operator Relasional pada Java
No
Operator
Contoh
1
==
(10 == 20) akan menghasilkan nilai FALSE
2
!=
(10 != 20) akan menghasilkan nilai TRUE
3
>
(10 > 20) akan menghasilkan nilai FALSE
4
<
(10 < 20) akan menghasilkan nilai TRUE
5
>=
(10 >= 20) akan menghasilkan nilai FALSE
6
<=
(10 <= 20) akan menghasilkan nilai TRUE


Referensi tulisan :
Trainer Enigmacamp Bpk. Yussin R. Hidayat
Docs.oracle.com
Gotutorid.com




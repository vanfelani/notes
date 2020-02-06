
# Expressions, Statements, and Blocks

1.  Expressions

Expression adalah hal – hal mendasar dalam proses perhitungan di dalam bahasa pemrograman. Expression adalah susunan yang terdiri dari operand dan operator.

Contoh :

int a = 7 \* 2 + 1;

2. Block

Block digunakan untuk mengelompokkan 0 atau lebih statement. Block dibuka dan ditutup oleh { }.

Contoh :

{

   _System.out.println(&quot;Lebih Kecil&quot;);_

}

3.  Statements

Sebuah statement dapat terdiri lebih dari satu baris. Setiap statement dapat berupa sebaris kode yang diakhiri dengan tanda ( ; ).


# IF - Else

Jika kondisi pertama tidak terpenuhi , maka kode program akan lanjut ke kondisi IF di bawahnya. Jika ternyata tidak juga terpenuhi, akan lanjut lagi ke kondisi IF di bawahnya, dst hingga blok ELSE terakhir atau terdapat kondisi IF yang bernilai true

public static void main(String[] args) {

        int a=20;

        if(a<18){

System.out.println("Lebih Kecil dari 18");

    }   else

{

System.out.println("Lebih Besar dari 18");

}

_Output : Lebih Besar dari 18_

#
**# Switch - Case**

Switch-case hampir sama seperti if – else, yang membedakannya switch-case hanya bisa dinyatakan dengan bilangan bulat atau karakter/string sedangkan  if -else yang dapat menggunakan operasi seperti <, >, <= dan >=. 
public class test {

    public static void main(String[] args) {

        int month = 8;

        String monthString;

        switch (month) {

            case 1:  monthString = "January";

                     break;

            case 2:  monthString = "Februari";

                     break;

            case 3:  monthString = "Maret";

                     break;

            case 4:  monthString = "April"

                     break;

            case 5:  monthString = "Mei"

                     break;

            case 6:  monthString = "Juni"

                     break;

            case 7:  monthString = "Juli"

                     break;

            case 8:  monthString = "Agust"

                     break;

            case 9:  monthString = "Septermber"

                     break;

            case 10: monthString = "Oktober"

                     break;

            case 11: monthString = "Novermber"

                     break;

            case 12: monthString = "Desember"

                     break;

            default: monthString = "Invalid month";
                     break;


                     break;

        }

        System.out.println(monthString);

    }

}

Output : August

Perintah **break** jika digunakan di dalam perulangan berfungsi untuk menghentikan paksa proses perulangan yang berlangsung.berbeda dengan Continue dia tidak akan menghentikan program saat dieksekusi misalnya menggunakan for loops tapi hanya akan melewatinya saja



# While &amp; do while

**A. while loop**

**while loop** digunakan untuk mengeksekusi kode program berulang-ulang sampai kondisi tertentu, cara penulisan syntax pada while, seperti ini:

while(boolean\_expression){

   //statement;

}

Pernyataan atau kode program didalam while akan terus di eksekusi berulang-ulang selama nilai pada boolean_expression bernilai "true", untuk menghentikan perulangan tersebut, kalian perlu memberikan pernyataan yang dapat mengubah boolean_expression menjadi "false". Contohnya seperti ini:

public class test {

    public static void main(String[] args) {
        String a = "Halo ";
        int jumlah = 0;
        while(jumlah < 5){
            System.out.println(a);
            jumlah++;
        }

}
}

**B. do-while**

do-while hampir sama dengan while, yang membedakannya adalah, while loop akan meihat kondisi boolean_expression terlehih dahulu, jika bernilai "true", maka pernyataan didalamnya akan dijalankan, berbeda dengan do-while, pada do-while, pernyataan akan di eksekusi terlebih dahulu sebelum mengevaluasi boolean_expression.
do{
   //statement;
}while(boolean_expression);

Coba kalian perhatikan kode program berikut ini, program akan mengeksekusi pernyataan didalam do terlebih dahulu, walaupun kondisi pada boolean_expressionnya bernilai "false",
public class latihan_looping {

    public static void main(String[] args) {
        String a = "hello";
        int x = 0;
        do{
            System.out.println(a);
            x++;
        }while(x > 9);} }

**For**

Penggunaan for hampir sama dengan kedua struktur perulangan sebelumnya yaitu while dan do-while, cara penulisan syntaxnya pun berbeda dengan kedua statement tersebut. tetapi memiliki fungsi yang sama yaitu untuk melakukan looping/perulangan sebanyak jumlah yang telah ditentukan.

for(inisialisasi_variable; kondisi; stepExpression){
  //statement
}



Ada tiga paramater yang umum digunakan untuk membuat for loop, yaitu:
•	inisialisasi_variable - menginisialisasi dari variable loop.
•	kondisi - membandingkan nilai pada variable loop dengan nilai batas, yang menghasilkan nilai boolean.
•	stepExression - melakukan update pada variable loop.

Contoh penggunaan for loops seperti berikut ini: 
public class test {

    public static void main(String[] args) {
        String a = "hallo";
        int jumlah = 5;
        for(int x=0; x<jumlah; x++){
            System.out.println(a);
        }
    }
}

Program tersebut akan menghasilkan output "Bisa" sebanyak 5 kali, pertama-tama, for akan melihat kondisi jika x lebih kecil dari 5 (jumlah) maka statement didalamnya akan dijalankan, setelah itu value pada variable x akan bertambah 1 (x++) sampai kondisi bernilai "false".




**OBJECT**

Objek adalah kunci untuk memahami teknologi berorientasi objek. contoh benda dunia nyata: anjing , meja, televisi, sepeda.

Objek dunia nyata memiliki dua karakteristik: Mereka semua memiliki keadaan dan perilaku. Anjing memiliki status (nama, warna, jenis, lapar) dan perilaku (menggonggong, mengambil, mengibaskan ekor). Sepeda juga memiliki status (gigi saat ini, irama pedal saat ini, kecepatan saat ini)

**Class**

Class adalah prototype, atau blueprint, atau rancangan yang mendefinisikan variable dan method-methode pada seluruh objek tertentu. Class berfungsi untuk menampung isi dari program yang akan di jalankan, di dalamnya berisi atribut / type data dan method untuk menjalankan suatu program.

**Inheritance**

Pewarisan/Penurunan adalah konsep pemrograman dimana sebuah class dapat ‘menurunkan’ property dan method yang dimilikinya kepada class lain. Konsep inheritance digunakan untuk memanfaatkan fitur ‘code reuse’ untuk menghindari duplikasi kode program.

**Package**

Package sebenarnya untuk memudahkan mengorganisir file dari class. Package ini merupakan suatu kelompok atau grup yang terdiri dari class – class, sub packages dan juga interfaces.

**Access Modifiers**
Public = bias diakses semua
Private = Cuma bias diakses didalam class itu sendiri

**Ovirride**
Ovirride membolehkan sebuah class mempunyai 2 atau lebih methode dengan nama yang sama, yang membedakannya adalah parameternya 

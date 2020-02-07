
# Method

## Definisi

Method adalah sarana bagi programmer untuk memodularisasi, artinya membreak atau memecah program kompleks menjadi bagian yang kecil-kecil sehingga nantinya dapat digunakan berulang-ulang, daripada menulis beberapa baris kode yang sama. Dan dibeberapa Bahasa Program Method ini juga disebut dengan Function seperti PHP,C++, dan lain-lain.

>untuk penamaan Method menggunakan Gaya Camel case seperti contoh : public static int metodeSaya() { [code] }

## Contoh

```java
public class Main {

    public static int penjumlahan(int x, int y) {
        return x + y;
    }

    public static void main(String[] args) {
        int a = 1;
        int b = 10;
        int hasil = penjumlahan(a, b);
        System.out.print(hasil);
    }

}
```

# Recursive Method

## Definisi

Recursive adalah Method yang dipanggil didalam Method itu sendiri, dengan kata lain method yang memanggil dirinya sendiri.

>Cara ini biasa digunakan untuk perulangan(looping).

## Contoh

```java
public class Main {

    static int factorial(int n) {
        if ( n == 1 )
            return 1;
        else
            return( n * factorial(n-1) );
    }

    public static void main(String[] args) {
        System.out.println("Factorial of 5 is: "+factorial(5));
    }
```
# Passing Parameter By Value and By Reference

**By Value** mendeklarasikan parameter inputan yang berupa variabel

**By Reference** mendeklarasikan parameter inputan yang berupa pointer


# Object

## Definisi

Object adalah hasil instantiate dari class. Karena class berbentuk “cetakan”, maka untuk mengambil isi cetakan tersebut kita wajib buat objectnya

## Contoh

```java
public class Main {

    public Main(){
        //membuat object "kucing" dari class Hewan
        //membuat object menggunakan keyword new
        Hewan kucing = new Hewan("Kucing", 4);

        //menjalankan method info
        kucing.info();
    }
    
    public static void main(String[] args) {
        new Main();
    }

    public class Hewan {
        //inisialisasi variabel untuk class Hewan
        int jumlahKaki = 0;
        String namaHewan = "";

        //constructor
        public Hewan(String nama, int kaki){
            this.jumlahKaki = kaki;
            this.namaHewan = nama;
        }

        //method untuk mengambil info nama dan jumlahkaki
        public void info(){
            System.out.println("Nama Hewan : "+this.namaHewan + ", Kaki : "+this.jumlahKaki);
        }
    }

}
```

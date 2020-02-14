# **I/O Stream**
Sebuah *stream* I / O  merupakan sumber input atau tujuan output. Sebuah *stream* dapat mewakili berbagai jenis sumber dan tujuan, termasuk file disk, perangkat, program lain, dan larik memori.

*stream* mendukung berbagai jenis data, termasuk byte sederhana, tipe data primitif, karakter lokal, dan objek. Beberapa aliran hanya meneruskan data; yang lain memanipulasi dan mengubah data dengan cara yang bermanfaat.

Program Java melakukan operasi i/o dengan menggunakan streams. Streams adalah abstraks dari sesuatu yang digunakan untuk menulis atau menghasilkan dan membaca atau mendapatkan suatu informasi.
Secara umum streams dalam Java dapat dibagi ke dalam dua bagian besar, yaitu:
- Byte streams
- Character streams

Semua class dan interface yang berhubungan dengan streams ada dalam package Java.io.

Tidak peduli bagaimana mereka bekerja secara internal, semua *stream* menyajikan model sederhana yang sama untuk program yang menggunakannya ; adalah urutan data. Suatu program menggunakan aliran input untuk membaca data dari sumber, satu per satu.

## Byte **Streams**

Program menggunakan byte *stream* untuk melakukan input dan output byte 8-bit. Semua byte *stream* kelas diturunkan dari Input *stream* dan Output *stream*.

Ada banyak kelas byte *stream*. Untuk mendemonstrasikan bagaimana fungsi dari byte *stream*, kita akan fokus pada file I / O byte *stream* , FileInput *stream* dan FileOutput *stream*. Jenis lain dari byte *stream*  digunakan dengan cara yang sama.

**Daftar class bertipe byte streams**
```java
BufferedInputStream
BufferedOutputStream
ByteArrayInputStream
ByteArrayOutputStream
DataInputStream
DataOutputStream
FileInputStream
FileOutputStream
PrintStream
```

## Character *Streams*
Platform Java menyimpan nilai karakter menggunakan konvensi *Unicode*. Character *stream* I / O secara otomatis menerjemahkan format internal ini ke dan dari set karakter lokal. Di negara Barat, set karakter lokal biasanya superset 8-bit ASCII.
Untuk sebagian besar aplikasi, I / O dengan karakter *streams* tidak lebih rumit dari I/O dengan byte *stream*. Input dan output dilakukan dengan kelas *stream* yang diterjemahkan secara otomatis dari rangkaian karakter lokal.
*Stream* ini digunakan untuk menulis maupun membaca data bertipe karakter. Character streams terdiri dari dua superclass, yaitu *Reader* dan *Writer*

**Daftar class bertipe character streams**
~~~~java
BufferedReader
BufferedWriter
CharArrayReader
CharArrayWriter
FileReader
FileWriter
InputStreamReader
OutpuStreamWriter
PrintWriter
StringReader
String Writer
~~~~

Semua karakter *Stream* kelas diturunkan dari *Reader* dan *Writer*. Seperti byte *streams*, ada kelas karakter *stream* yang spesifik dalam file I / O: *FileReader* dan *FileWriter*.

### Character *streams* that Use Byte *streams*
Karakter *stream*  seringkali menjadi "pembungkus" untuk byte *streams*. Karakter *stream* menggunakan byte *stream* untuk melakukan I / O, sedangkan karakter *stream* menangani terjemahan antara karakter dan byte. 
*FileReader*, misalnya, menggunakan *FileInput* *stream*, sedangkan *FileWriter* menggunakan *FileOutput* *stream*.

## Line-Oriented I/O

Karakter I / O biasanya terjadi dalam satuan yang lebih besar daripada karakter tunggal. Satu unit yang umum adalah baris: serangkaian karakter dengan terminator garis di akhir. Terminator garis dapat berupa urutan :

- *carriage-return / feed-feed ("\ r \ n")*
- *carriage-return tunggal ("\ r")* atau 
- *feed-line tunggal ("\ n")* 

Mendukung semua terminator garis yang memungkinkan memungkinkan program membaca file teks yang dibuat pada salah satu sistem operasi yang banyak digunakan.

*CopyCharacters* untuk menggunakan I / O berorientasi garis. Untuk melakukan ini, kita harus menggunakan dua kelas, *BufferedReader* dan *PrintWriter*.

Contoh *CopyLines* memanggil *BufferedReader.readLine* dan *PrintWriter.println* untuk melakukan input dan output satu baris pada satu waktu : 
~~~~java
import java.io.FileReader;
import java.io.FileWriter;
import java.io.BufferedReader;
import java.io.PrintWriter;
import java.io.IOException;

public class CopyLines {
    public static void main(String[] args) throws IOException {

        BufferedReader inputStream = null;
        PrintWriter outputStream = null;

        try {
            inputStream = new BufferedReader(new FileReader("xanadu.txt"));
            outputStream = new PrintWriter(new FileWriter("characteroutput.txt"));

            String l;
            while ((l = inputStream.readLine()) != null) {
                outputStream.println(l);
            }
        } finally {
            if (inputStream != null) {
                inputStream.close();
            }
            if (outputStream != null) {
                outputStream.close();
            }
        }
    }
}
~~~~

Ada banyak cara untuk menyusun input dan output teks di luar karakter dan garis. Untuk informasi lebih lanjut, lihat Memindai dan Memformat.

## Buffered *streams*

Sebagian besar contoh yang telah kita lihat sejauh ini menggunakan I / O tanpa buffer. Ini berarti setiap permintaan baca atau tulis ditangani langsung oleh OS yang mendasarinya. Ini dapat membuat program menjadi kurang efisien, karena setiap permintaan seperti itu sering memicu akses disk, aktivitas jaringan, atau operasi lain yang relatif mahal.

### Flushing Buffered *streams*

Seringkali masuk akal untuk menulis buffer pada titik-titik kritis, tanpa menunggu untuk mengisi. Ini dikenal sebagai *flushing buffer*.
Beberapa kelas output yang disangga mendukung *autoflush*, ditentukan oleh argumen konstruktor opsional. Sebagai contoh, objek *PrintWriter autoflush flush buffer* pada setiap permintaan *println* atau format.

Untuk *mem-flush stream* secara manual, aktifkan metode *flush-nya*. Metode *flush* berlaku pada output *stream* apa pun, tetapi tidak berpengaruh kecuali *stream buffered*.

## Scanning and Formatting

Pemrograman I / O sering melibatkan penerjemahan ke dan dari data yang akan digunakan untuk mempermudah tugas. Untuk membantu dalam mempermudah tugas, platform Java menyediakan dua API. API pemindai memecah input menjadi token individual yang terkait dengan bit data. API pemformatan mengumpulkan data ke dalam format yang diformat dengan baik, dapat dibaca manusia.

### Scanning

Tipe Scanning berguna untuk memecah input yang diformat menjadi penanda dan menerjemahkan masing-masing penanda sesuai dengan tipe datanya.

Memecah Input menjadi penanda
Secara default, pemindai menggunakan *whitespace* untuk memisahkan penanda. Karakter *whitespace* menyertakan blank, tab, dan terminator garis. Untuk daftar lengkap, lihat dokumentasi untuk `Character.isWhitespace`.
Untuk menggunakan pemisah penanda yang berbeda, aktifkan useDelimiter (), tentukan ekspresi reguler. Misalnya, Anda ingin pemisah token menjadi koma, opsional diikuti oleh *whitespace*. 

  ```s.useDelimiter (", \\ s *"); ```


 ex :



## I/O dari Command Line

Sebuah program yang sering dijalankan dari baris perintah dan berinteraksi dengan pengguna di sekitar baris perintah. Platform Java mendukung interaksi semacam ini dalam dua cara: melalui Standard *streams* and *through the Console*.

### Standard *streams*

Standard *stream* adalah fitur dari banyak sistem operasi. Secara default, mereka membaca input dari keyboard dan menulis output ke layar. Mereka juga mendukung I / O pada file dan antar program, tetapi fitur itu dikendalikan oleh penerjemah baris perintah, bukan program.
Platform Java mendukung tiga *stream* standar :

- Standard Input, accessed through System.in; 
- Standard Output, accessed through System.out; dan
- Standard Error, accessed through System.err

Objek-objek ini didefinisikan secara otomatis dan tidak perlu dibuka. *Standar Output* dan *Standar Error*  keduanya untuk output; memiliki output kesalahan secara terpisah memungkinkan pengguna untuk mengalihkan output reguler ke file dan masih dapat membaca pesan kesalahan.
Sebaliknya, `System.in` adalah byte *stream* tanpa fitur karakter *stream*. Untuk menggunakan *Standar Input* sebagai karakter *stream*, yang dibungkus dalam `System.in` dalam Input *streamReader*.
```InputstreamReader cin = new Input*stream*Reader(System.in);```


## Data *Stream*

Data *stream* mendukung biner I / O dari nilai tipe data primitif (boolean, char, byte, short, int, long, float, dan double) serta nilai String. Semua data *stream* mengimplementasikan interface DataInput atau interface DataOutput. Bagian ini berfokus pada implementasi interface yang paling banyak digunakan, DataInput *stream* dan DataOutput *stream*.

Contoh data *stream* yang menunjukkan data *streams* dengan menulis satu set catatan data, dan kemudian membacanya lagi. Setiap catatan terdiri dari tiga nilai yang terkait dengan item pada faktur, seperti yang ditunjukkan pada tabel berikut:


| Order in record | Data type | Input Method                  | Output Method               | Sample Value |
| --------------- | --------- | ------------------------------| ----------------------------| ------------ |
| 1               | double    | DataOutput*stream*.writeDouble| DataInput*stream*.readDouble| 19.99        |
| 2               | int       | DataOutput*stream*.writeInt   | DataInput*stream*.readInt   | 12           |
| 3               | String    | DataOutput*stream*.writeUTF   | DataInput*stream*.readUTF   | "Java T-Shirt|







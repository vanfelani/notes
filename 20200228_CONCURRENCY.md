# **CONCURRENCY**

## Pendahuluan

Platform Java dirancang dari bawah ke atas untuk mendukung pemrograman bersamaan, dengan dukungan konkurensi dasar dalam bahasa pemrograman Java dan perpustakaan kelas Java. 
Sejak versi 5.0, platform Java juga menyertakan API konkurensi tingkat tinggi. 
Pelajaran ini memperkenalkan dukungan konkurensi dasar platform dan merangkum beberapa API tingkat tinggi dalam java.util.concurrentpaket.



### Procceses & Threads

1. Procceses :
Proses sering dianggap identik dengan program atau aplikasi. Namun, apa yang dilihat pengguna sebagai satu aplikasi mungkin sebenarnya adalah serangkaian proses kerja sama. Untuk memfasilitasi komunikasi antar proses, sebagian besar sistem operasi mendukung sumber daya Inter Process Communication (IPC), seperti pipa dan soket. 
IPC digunakan tidak hanya untuk komunikasi antar proses pada sistem yang sama, tetapi proses pada sistem yang berbeda, Sebagian besar implementasi mesin virtual Java dijalankan sebagai satu proses.

2. Threads : 
Thread kadang-kadang disebut proses ringan. 
Baik proses maupun Thread menyediakan lingkungan eksekusi, tetapi membuat Thread baru membutuhkan sumber daya yang lebih sedikit daripada membuat proses baru. 
Thread ada dalam suatu proses - setiap proses memiliki setidaknya satu. Thread membagikan sumber daya proses, termasuk memori dan file yang terbuka. Ini membuat komunikasi menjadi efisien, tetapi berpotensi bermasalah.

#### a. Memulai Thread

Ada 2 cara untuk membuat perintah Thread

* Menggunakan Runnable

```
public class HelloRunnable implements Runnable {

    public void run() {
        System.out.println("Hello from a thread!");
    }

    public static void main(String args[]) {
        (new Thread(new HelloRunnable())).start();
    }

}
```

* Menggunakan Thread

```
public class HelloThread extends Thread {

    public void run() {
        System.out.println("Hello from a thread!");
    }

    public static void main(String args[]) {
        (new HelloThread()).start();
    }

}
```

Runnable lebih baik digunakan karena Runnable dapat digunakan
dibanyak kelas. Sedangkan Thread tidak dan lebih banyak digunakan pada progam yang sederhana.

#### b. Thread Sleep

Thread.sleep dapat membuat thread yang akan dijalankan akan ditunda eksekusinya. Ini adalah cara yang sangat efisien
untuk membuat waktu prosesor untuk menjalankan aplikasi yang menggunakan perintah thread.

Contoh penggunaannya:

```
public class SleepMessages {
    public static void main(String args[])
        throws InterruptedException {
        String importantInfo[] = {
            "Mares eat oats",
            "Does eat oats",
            "Little lambs eat ivy",
            "A kid will eat ivy too"
        };

        for (int i = 0;
             i < importantInfo.length;
             i++) {
            //Pause for 4 seconds
            Thread.sleep(4000);
            //Print a message
            System.out.println(importantInfo[i]);
        }
    }
}
```

#### b. Thread Interrupted

Penggunaan interrupted biasanya digunakan untuk menghentikan Thread yang dijalankan. 

Contoh penggunaannya:

```
    System.out.println("BEFORE START");
    MyThread mt1 = new MyThread(1,100);
    mt1.setName("Thread 1");
    MyRunnable r = new MyRunnable(101, 200);
    Thread mt2 = new Thread(r, "Thread 2");
    mt1.start();
    mt2.start();
    Thread.sleep(2000);
    mt1.interrupt(); // Penggunaan Interrupt
    System.out.println("AFTER START");
```
Maka hasilnya akan seperti ini:
```
AFTER START
java.lang.InterruptedException: sleep interrupted
	at java.base/java.lang.Thread.sleep(Native Method)
	at com.code.concurrency.MyThread.run(MyThread.java:63)
```
#### c. Thread Joins

Metode ini memungkinkan satu thread untuk menunggu thread yang lainnya.

Contoh penggunaannya :

```
System.out.println("BEFORE START");
          
          MyThread mt1 = new MyThread(1,100);
          mt1.setName("Thread 1");
          
          MyRunnable r = new MyRunnable(101, 200);
          Thread mt2 = new Thread(r);
          
          Thread[] threads = {mt1 ,mt2};
          
          for (Thread thread : threads) {
            thread.start();
          }
          
          for (Thread thread : threads) {
            thread.join(); //Penggunaan Join
              System.out.println(thread.getName() + " Done.");
          }
          
          System.out.println("AFTER START");
```

### Synchronization

Thread berkomunikasi terutama dengan berbagi akses ke bidang dan bidang referensi objek merujuk. Bentuk komunikasi ini sangat efisien, tetapi memungkinkan dua jenis kesalahan: interferensi utas dan kesalahan konsistensi memori . 
Alat yang diperlukan untuk mencegah kesalahan ini adalah sinkronisasi .

Namun, sinkronisasi dapat memperkenalkan Thread Contention , yang terjadi ketika dua atau lebih Thread mencoba mengakses sumber yang sama secara bersamaan dan menyebabkan Java runtime mengeksekusi satu atau lebih utas lebih lambat, atau bahkan menunda eksekusi mereka. Starvation dan livelock adalah bentuk thread contention.

#### a. Thread Interference
Disini terlebih dahulu membuat class counter:
```
class Counter {
    private int c = 0;

    public void increment() {
        c++;
    }

    public void decrement() {
        c--;
    }

    public int value() {
        return c;
    }

}
```
 Misalkan Thread A memanggil increment pada saat yang sama Thread B memanggil decrement. Jika nilai awal cadalah 0, tindakan mereka yang disisipkan mungkin mengikuti urutan ini:
 
 1. Thread A: Retrieve c.
 2. Thread B: Retrieve c.
 3. Thread A: Peningkatan nilai yang diambil; hasilnya adalah 1.
 4. Thread B: Pengurangan nilai yang diambil; hasilnya -1.
 5. Thread A: Simpan hasil dalam c; c sekarang 1.
 6. Thread B: Simpan hasil dalam c; c sekarang -1.
 
 Hasil Thread A hilang dan ditimpa oleh Thread B. Interleaving khusus ini hanya satu kemungkinan. Dalam keadaan yang berbeda, mungkin hasil Thread B yang hilang, atau tidak ada kesalahan sama sekali. Karena tidak dapat diprediksi.
 
 #### b. Memory Consistency Errors

Ada kemungkinan dimana perubahan yang dilakukan oleh satu Thread yang mungkin tidak terlihat oleh Thread lainnya dan semuanya memiliki pandangan yang tidak konsisten dari data yang sama.

Tindakan berikut dapat menghindari Memory Consistency Errors:

Thread.start () - Pernyataan ini membuat efek kode yang mengarah pada pembuatan Thread baru terlihat oleh Thread lainnya.
Thread.join () - Pernyataan ini membuat efek kode di Thread terlihat oleh Thread yang melakukan penggabungan.

#### c. Synchronized Methods

Bahasa pemrograman Java menyediakan dua idiom sinkronisasi dasar: synchronized methods dan synchronized statements.

Contoh penggunaannya:

```
public class SynchronizedCounter {
    private int c = 0;

    public synchronized void increment() {
        c++;
    }

    public synchronized void decrement() {
        c--;
    }

    public synchronized int value() {
        return c;
    }
}
```

#### d. Atomic Access

Dalam pemrograman, aksi atom adalah tindakan yang secara efektif terjadi sekaligus. Tindakan atom tidak bisa berhenti di tengah: itu bisa terjadi sepenuhnya, atau tidak terjadi sama sekali. Tidak ada efek samping dari aksi atom yang terlihat sampai aksi selesai.

Adapun contoh variabel dari atomic, diantaranya:
1. AtomicBoolean
2. AtomicInteger
3. AtomicLong
4. AtomicReference

dan masih banyak lagi, bisa dilihat di : 
https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/atomic/package-summary.html

### Liveness

Kemampuan aplikasi bersamaan untuk mengeksekusi pada waktu yang tepat dikenal sebagai liveness. 
Bagian ini menjelaskan jenis masalah Liveness yang paling umum, Deadlock dan Starvation dan Livelock.

#### a. Deadlock

Deadlock dapat terjadi dalam situasi ketika Thread sedang menunggu kunci objek, yang diakuisisi oleh Thread lain dan utas Thread menunggu kunci objek yang diperoleh oleh Thread pertama. 
Karena, kedua Thread saling menunggu untuk diproses.

Contoh Deadlock:

```
public class Deadlock {
    static class Friend {
        private final String name;
        public Friend(String name) {
            this.name = name;
        }
        public String getName() {
            return this.name;
        }
        public synchronized void bow(Friend bower) {
            System.out.format("%s: %s"
                + "  has bowed to me!%n", 
                this.name, bower.getName());
            bower.bowBack(this);
        }
        public synchronized void bowBack(Friend bower) {
            System.out.format("%s: %s"
                + " has bowed back to me!%n",
                this.name, bower.getName());
        }
    }

    public static void main(String[] args) {
        final Friend alphonse =
            new Friend("Alphonse");
        final Friend gaston =
            new Friend("Gaston");
        new Thread(new Runnable() {
            public void run() { alphonse.bow(gaston); }
        }).start();
        new Thread(new Runnable() {
            public void run() { gaston.bow(alphonse); }
        }).start();
    }
}
```

Saat Deadlock dijalankan, sangat mungkin kedua Thread akan memblokir ketika mereka mencoba untuk memohon bowBack. Tidak ada blok yang akan berakhir, karena setiap Thread menunggu yang lain untuk keluar bow.

#### b. Starvation and Livelock

##### b.1 Starvation

Starvation menggambarkan situasi dimana Thread tidak dapat memperoleh akses reguler ke sumber daya bersama dan tidak dapat membuat kemajuan. 
Ini terjadi ketika sumber daya bersama tidak tersedia untuk jangka waktu lama karena ada Thread yang lain.

Sebagai contoh, misalkan suatu objek menyediakan metode yang disinkronkan yang seringkali membutuhkan waktu lama untuk kembali. Jika satu Thread sering menggunakan metode ini, 
Thread yang lainnya juga perlu disinkronkan ke objek yang sama akan diblokir.

##### b.2 Livelock

Sebuah Thread sering bertindak sebagai respons terhadap tindakan Thread lain. Jika tindakan Thread lainnya juga merupakan respons terhadap tindakan Thread lain, maka livelock dapat terjadi. Seperti halnya jalan buntu, Thread yang tidak dapat membuat kemajuan lebih lanjut. Namun, Thread tidak diblokir - mereka terlalu sibuk merespons satu sama lain untuk melanjutkan proses. 

Ini sebanding dengan dua orang yang mencoba saling melewati di koridor: Alphonse bergerak ke kiri untuk membiarkan Gaston lewat, sementara Gaston bergerak ke kanannya untuk membiarkan Alphonse lewat. Melihat bahwa mereka masih saling menghalangi, Alphone bergerak ke kanan, sementara Gaston bergerak ke kiri. dan mereka berjalan bersamaan.

### Guarded Block

Thread sering kali harus mengoordinasikan tindakan mereka. cara yang paling umum adalah Guarded Block. Blok seperti itu dimulai dengan suatu kondisi yang harus benar sebelum blok dapat dilanjutkan. Ada sejumlah langkah yang harus diikuti untuk melakukan ini dengan benar.

Misalkan, misalnya guardedJoy adalah metode yang tidak boleh dilanjutkan sampai variabel yang dibagi joy telah disetel oleh Thread lainnya. 
Metode seperti itu, secara teori, hanya mengulang sampai kondisi terpenuhi, tetapi loop itu sia-sia, karena dijalankan terus menerus sambil menunggu.

```
public void guardedJoy() {
    // Simple loop guard. Wastes
    // processor time. Don't do this!
    while(!joy) {}
    System.out.println("Joy has been achieved!");
}   
```

Guarded Block lebih efisien meenggunakan Object.wait untuk menangguhkan Thread saat ini. Perintah wait tidak akan kembali sampai Thread lainnya kita menggunakan perintah notify() atau notifiAll().

```
public synchronized void guardedJoy() {
    // This guard only loops once for each special event, which may not
    // be the event we're waiting for.
    while(!joy) {
        try {
            wait();
        } catch (InterruptedException e) {}
    }
    System.out.println("Joy and efficiency have been achieved!");
}
//Penggunaan notify
public synchronized notifyJoy() {
    joy = true;
    notifyAll();
}
```

### Immutable Object

Suatu objek dianggap tidak berubah jika kondisinya tidak dapat berubah setelah dibangun. Ketergantungan maksimum pada objek yang tidak dapat diubah diterima secara luas sebagai strategi yang bagus untuk membuat kode yang sederhana dan andal.

Objek yang tidak dapat berubah sangat berguna dalam aplikasi berbarengan. Karena mereka tidak dapat mengubah keadaan, mereka tidak dapat rusak oleh gangguan utas atau diamati dalam keadaan tidak konsisten.

### Executors

#### a. Executor Interfaces

Dalam java.util.concurrent package ada 3 jenis executor interfaces, yaitu :
1. Executor, perintah ini mendukung peluncuran tugas baru
2. ExecutorService, ini merupakan subinterface dari Executor, yang menambahkan fitur yang membantu mengelola siklus hidup, baik tugas individu maupun pelaksana itu sendiri.
3. ScheduledExecutorService, subinterface dari ExecutorService, mendukung pelaksanaan tugas di masa depan dan / atau berkala.

#### b. Thread Pools

Kumpulan thread menggunakan kembali thread yang telah dibuat sebelumnya untuk menjalankan tugas saat ini dan menawarkan solusi untuk masalah overhead siklus ulir dan perusakan sumber daya. Karena thread sudah ada saat permintaan tiba, 
penundaan yang diperkenalkan oleh pembuatan utas dihilangkan, membuat aplikasi lebih responsif.

Cara sederhana untuk membuat executor yang menggunakan thread pool tetap adalah dengan memanggil newFixedThreadPoolmetode pada java.util.concurrent.Executors, kelas ini juga menyediakan metode berikut:
1. newCachedThreadPool, Metode menciptakan pelaksana dengan thread pool yang banyak. Eksekutor ini cocok untuk aplikasi yang meluncurkan banyak tugas yang berumur pendek.
2. The newSingleThreadExecutor, Metode menciptakan executor yang mengeksekusi satu tugas pada satu waktu.
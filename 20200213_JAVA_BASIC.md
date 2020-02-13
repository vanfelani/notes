# Collections

*Collections* atau biasa disebut juga *container* adalah sebuah *object* yang mengelompokan beberapa *elements* ke dalam satu unit. *Collections* digunakan untuk mengambil, menyimpan, memanipulasi, dan menghubungkan *aggregate data*. Khususnya, *collections* menunjukan data *items* yang membentuk *natural group*, seperti kartu remi (sekumpulan kartu), *mail folder*(sekumpulan surat), atau buku telepon(pemetaan nama pada nomor telfon).

## Collections Frameworks
Collections frameworks adalah arsitektur terpadu untuk menampilkan dan manipulasi *collections*. Berikut adalah komponen-komponen dari *collections framework*:

- *Interfaces* : *interface* merupakan data yang bertipe abstrak yang menggambarkan *collections*. *Interface* memperboldehkan *collections* untuk diubah atau dimanipulasi bentuk penggambarannya secara bebas. pada bahasa pemograman berorientasi obyek, *interface* pada umumnya berbentuk hirarki.
- Implementasi: Di dalamnya terdapat bentuk konkrit pengimplementasian dari *collections interface*. Pada intinya, *collections* bisa digunakan secara berulangkali.
- Algoritma: merupakan metode yang menghasilkan komputasi yang berdaya guna, seperti *searching*(pencarian) dan *sorting*(pengurutan), pada obyek yang mengimplementasi *interface*. Algoritma dikatakan polimorfik yang mana bisa menggunakan metode yang sama pada implementasi yang berbeda -beda dari *collection Interface* yang sesuai. 

adapun keuntungan dari penggunakan *java collections framework* yaitu:

- mengurangi upaya dalam melakukan program yang berat.
- meningkatkan kecepatan dan kualitas program.
- mengizinkan relasi antar API yang tidak berkaitan (fleksibel).
- mengurangi upaya untuk membuat atau menggunakan API baru.
- dapat digunkan berulang kali. 



## Core Collection Interfaces 

*Core Collection Interfaces* merangkum berbagai jenis *collections*, yang mana dapat kita lihat pada Figure 1. Seperti yang kita lihat *core collections* dapat dibentuk secara hirarki. 

![Figure 1](https://www.startertutorials.com/corejava/wp-content/uploads/2018/02/collections-hierarchy.png)

*Set* merupakan jenis khusus dari *collection*, *SortedSet* adalah jenis khusus dari *set*, dan seterusnya. Perhatikan bahwa urutan tingkatan mengandung dua pohon yang berbeda, satu lagi *Map*. Map sejatinya bukan bukan termasuk kedalam pohon *collection*.



Perhatikan bahwa semua inti dari *collection interfaces* merupakan *generic*. untuk contoh, berikut adalah deklarasi dari *collection interface*.

```java
public interface Collection<E>...
```

syntax `<E>` melambangkan bahwa *interface* ini merupakan memiliki sifat generik. Saat mendeklarasi sebuah *instance* dari *Collection* kita harus memberi tipe yang spesifik pada obyek yang terkandung di dalam *collection*. 



### Collection Interface

Merupakan akar dari bentuk tingkat (hirarki) *collection*. *collection* menunjukan sebuah kelompok dari obyek yang kita bisa kenal sebagai *elements*. *Collection interface* adalah bentuk dominan semua implementasi *collections* dan digunakan untuk  melewati dan memanipulasi *collections* apa saja yang ada jika saat generalisasi yang maksimum diinginkan. Beberapa tipe *collection* ada yang bisa mempunyai *element*-yang duplicat ada yang tidak bisa, ada yang bisa berurut dan ada juga yang tidak bisa.  *Java platform*  tidak menyediakan akses untuk langsung mengimplementasikan *interface* ini tetapi *java platform* menyediakan implementasi melalui sub-*interface*-nya , seperti *list* dan *set*.

contoh pengimplementasian dari *interface collection* adalah sebagai berikut:

seumpama kita memiliki `Collection<String> c`, yang mana mungkin itu bisa menjadi *list*, *set*, atau jenis *collection* yang lainnya. Code diatas akan membuat *ArrayList* (jenis implementasi dari *interface* list) baru.

````java
List<String> list = new ArrayList<>(c);
````

*collection interface* memiliki methods yang menghasilkan operasi dasr, seperti `int size(), boolean isEmpty(), boolean contains(Object elemnt), boolean add(E element), boolean remove(Object element),` dan `Iterator<E>`. *collection*s juga mengandung operasi yang dapat mengoperasikan semua *collections* seperti `containAll(Collection<?> c), boolean addAll.., boolean removeAll.., boolean retain All`, dll.



#### Berbagai cara untuk *Traversing Collection* 

Ada tiga cara untuk *traverse collections* :

- Operasi Agregat

  pada JDK versi 8 dan diatasnya, metode yang dianjurkan untuk melakukan iterasi pada antar *collection* adalah menggunakan *stream* dan melakukan operasi agregat di dalamnya. Contohnya kita bisa lihat dibawah.

  ~~~~java
  List<Box> list = ArrayList<>();
  list.stream()
  	.filter(e -> e % 2 == 1); 
  	.foeEach(e -> System.out.println(e));
  ~~~~

  code di atas melakukan iterasi menggunakan stream serta terdapat operasi agregat di dalamnya untuk mencari element yang bersifat genap di dalam list lalu menampilkannya.

- Konstruksi *For-each*

  konstruksi *for-each* mengizinkan untuk *traverse* sebuah *collection* atau array secara singkat menggunkan perulangan for. Sebagai contoh

  ~~~~java
  for (Object o : collection)
      System.out.println(o);
  ~~~~

- Iterators

  Iterator adalah sebuah obyek yang mana memungkinkan untuk *traverse* melalui *collection* dan menghapus *elemnts* dari *collection* secara selektif. Contohnya:

  ~~~~java
  public interface Iterator<E> {
      boolean hasNext();
      E next();
      void remove(); //optional
  }
  ~~~~

  Method `hashNext` mengembalikan nilai `true` jika iterasinya mempunyai element yang lebih (mengecek element disebelahnya).  Method `remove`untuk menghapus *elements*. 

  Berikut contoh implementasi menghapus elements yang bernilai genap dari list: 

  ````java
  for(Iterator<Integer> it = list.iterator(); it.hasNext(); ){
  	Integer n = it.next();
  	if (n %2 == 0){
  		it.remove();
  	}
  }
  ````

  

#### Operasi Jumlah Besar dalam Collections Interface (Bulk Operation)

*Bulk operation* melakukan sebuah operasi pada semua *collection*. berikut adalah *bulk operation* :

- `containsAll` : mengembalikan nilai true jika target *collection* mengandung semua elements di dalam *collection* yang ditentukan.

- `addAll`: menambahkan semua elemnts di dalam *collection* yang ditentukan ke dalam *collection* target.

- `removeAll`: menghapus semua elements dari *collection* target yang mana juga terdapat pada *collection* yang ditentukan.

- `retainAll`:  menghapus semua elements dari *collection* target yang mana tidak terdapat di dalam *collection* yang ditentukan.

- `clear`: menghapus semua elemnts dari *collection*.

  

#### Operasi Array dalam Collection Interface 

Metode `toArray` merupakan metode yang menjembatani antara *collections* dan APIs versi dahulu yang hanya menerima input array. Operasi array dapat membuat konten dari *collection* berubah menjadi array. Sebagai contoh diberikan `c` sebagai *collection*.

````java
Object[] a = c.toArray();
````

code di atas menjadikan konten dari `c` menjadi array obyek baru yang sudah teralokasi yang mana panjangnya sama dengan jumlah elements di dalam `c`.



### Set Interface

Set merupakan *collection* yang tidak bisa mengandung element yang ganda. Sifatnya mirip dengan model himpunan abstraks matematika. Pada *java platform* ada tiga bentuk pengimplementasian dari *Set*, yaitu: 

- `HashSet`: Perurutan set random/ada algortma sendiri dari *java platform*.

- `TreeSet`: Perurutan set sesuai natural order. `TreeSet` mengimplementasi *interface* dari *sortedList*. 

- `LinkedHashSet`: Perurutan list secara FIFO (*first in, first out*).

  

#### Operasi Dasar dari Interface Set

Operasi `size` mengembalikan jumlah nilai dari elements yang ada di dalam set (kardinalitas). Metod `isEmpty` untuk mengencek apakah sebuah set kosong atau tidak. Metod `add` untuk menambahkan elements yang ditentukan ke dalam set dan akan mengembalikan nilai boolean jika element sukses atau tidak sukses ditambahkan. 

Berikut merupakan contoh dari program menggunakan operasi agregat yang menampilkan semua kata yang berbeda dalam setiap argumen list.

````java
import java.util.*;
import java.util.stream.*;

public class FindDups {
    public static void main(String[] args) {
        Set<String> distinctWords = Arrays.asList(args).stream()
		.collect(Collectors.toSet()); 
        System.out.println(distinctWords.size()+ 
                           " distinct words: " + 
                           distinctWords);
    }
}
````



#### Operasi Jumlah Besar dalam Set Interface

Operasi *bulk* sangat cocok diterapkan pada interface *set*, ketika diterapkan akan menghasilkan standar himpunan operasi aljabar. Diberikan himpunan `s1` dan `s2 maka ini yang akan dilakukan operasi *bulk*:

- `s1.containsAll(s2)` : mengembalikan nilai `true` jika `s2` adalah himpunan irisan dari `s1`.
- `s1.addAll(s2)`: mengubah `s1` menjadi himpunan gabungan dari `s1`dan`s2`.
- `s1.retainAll(s2)`: mentransformasikan `s1` ke persimpangan `s1` dan `s2`. (Perpotongan dua set adalah set yang hanya berisi elemen yang sama untuk kedua set.)
- `s1.removeAll(s2)` - mentransformasikan `s1` menjadi set perbedaan (asymmetric) dari `s1` dan `s2`. (Misalnya, perbedaan himpunan `s1` minus `s2` adalah himpunan yang berisi semua elemen yang ditemukan dalam `s1` tetapi tidak dalam `s2`).



### List Interface

*List* merupakan *collection* yang terurut(*sequence*). List bisa mengandung elements ganda. Untuk tambahan operasi yang mewarisi dari *collection*, list interface mengandung operasi sebagai berikut:

- `Positional access`: memanipulasi elemen berdasarkan posisi numerik mereka dalam list. Ini termasuk metode seperti `get`, `set`, `add`, `addAll`, dan `remove`.
- `Search`: Mencari objek tertentu dalam list dan mengembalikan posisi numeriknya. Metode pencarian termasuk `indexOf` dan `lastIndexOf`.
- `Iteration`: memperluas semantik Iterator untuk mengambil keuntungan dari sifat berurutan list. Metode list Iterator menyediakan fitur ini.
- `Range`: Metode sublist melakukan operasi rentang sewenang-wenang pada list.



##### Operasi Akses Posisi dan Pencarian

Operasi dasar dari akses posisi adalah `get`,`set`, `add`, dan `remove` yang mana mengambalikan nilai lama yang telah ditimpa atau dihapus. Operasi lain seperti `indexOf` dan `lastIndexOf` mengembalikan index pertam dan terakhir dari element di dalam list.

Contoh metod sedrhana *swap* dua nilai index di dalam list.

````java
public static <E> void swap(List<E> a, int i, int j) {
    E tmp = a.get(i);
    a.set(i, a.get(j));
    a.set(j, tmp);
}
````



#### Range-View Operation

Operasi range-view, subList (`int dariIndex, int toIndex`), mengembalikan tampilan list bagian dari list ini yang indeksnya berkisar dari `fromIndex`, inklusif, hingga `toIndex`, eksklusif. Rentang setengah terbuka ini mencerminkan tipikal untuk loop.



#### Algoritma List

- `sort` - Mengurutkan list yang menggunakan algoritma sortir gabungan, yang menyediakan sortir yang cepat dan stabil. (Jenis stabil adalah yang tidak menyusun ulang elemen yang sama).
- `shuffle` - Dengan acak memutasi element yang ada di dalam list.
- `reverse` - Membalikan urutan dari elemnt di dalam list.
- `rotate` - Memutar semua element di dalam list.
- `swap` - Menukar element dengan posisi yang ditentukan di dalam list.



### Queue Interface

Queue(antrian) merupakan *collection* yang menampung elements sebelum diproses. Selain dari operasi dasar *collection*, queue mempunyai operasi tambahan seperti `insertion`,`removal`, dan `inspection operations`.

setiap method dalam queue memiliki dua bentuk: (1) satu melempar sebuah *exception* jika operasi gagal, dan (2) mengembalikan nilai spesial jika operasi gagal (`null` maupun `false`, tergantung operasinya).

| Tipe Operasi | Throws exception | Return special value |
| ------------ | ---------------- | -------------------- |
| `insert`     | `add(e)`         | `offer(e)`           |
| `remove`     | `remove()`       | `poll()`             |
| `Examine`    | `element()`      | `peek()`             |

 

### Deque Interface

Biasanya diucapkan sebagai dek, deque adalah queue ujung ganda. queue berujung ganda adalah kumpulan linier elemen yang mendukung penyisipan dan penghapusan elemen di kedua titik akhir. Deque interface adalah tipe data abstrak yang lebih kaya daripada Stack dan Queue karena mengimplementasikan kedua tumpukan dan antrian pada saat yang sama. Antarmuka Deque, mendefinisikan metode untuk mengakses elemen di kedua ujung instance Deque. Metode disediakan untuk menyisipkan, menghapus, dan memeriksa elemen. Kelas standar seperti ArrayDeque dan LinkedList mengimplementasikan Deque Interface.

​																			Deque Method

| Tipe Operasi | Element Pertama                | Element Terakhir             |
| ------------ | ------------------------------ | ---------------------------- |
| `Insert`     | `addFirst(e)`                  | `addLast(e)`,`offerLast(e)`  |
| `Remove`     | `removeFirst()`, `pollFirst()` | `removeLast()`, `pollLAst()` |
| `Examine`    | `getFirst()`, `peekFirst()`    | `getLast()`,`peekLast(`)     |



### Map Interface

Map adalah objek yang memetakan kunci nilai. Peta tidak dapat berisi kunci duplikat: Setiap kunci dapat memetakan paling banyak satu nilai. Ini memodelkan abstraksi fungsi matematika. Antarmuka Peta mencakup metode untuk operasi dasar (seperti menempatkan, mendapatkan, menghapus, berisiKey, berisi Nilai, ukuran, dan kosong), operasi massal (seperti putAll dan clear), dan tampilan kumpulan (seperti keySet, entrySet, dan nilai) .

*Java platform* memiliki tiga implementasi umum dari Map, yaitu: `HashMap`, `TreeMap`, dan `LinkedHashMap`. Ciri-cirinya mirip dengan `HashSet`, `TreeSet`, dan `LinkedHashSet` yang telah dijelaskan dalam sub bab Set Interface.



#### Operasi Dasar Map Interface

Operasi dasar dari Map (`put, get, containsKey, containsValue, size,` dan `isEmpty`) mempunyai ciri yang mirip dengan `Hashtable`. 

Contoh program menggunkan implementasi `HashMap`, `TreeMap`, dan `LinkedHashMap` dari map adalah sebagai berikut:

````java
Map<String, String>map1 = new HashMap<>();
map1.put("bcd", "bcd");
map1.put("def", "bcd");
map1.put("abc", "bcd");

Map<string, string> map2 = TreeMap<>(map1);
Map<string, string> map3 = LinkedHashMap<>(map1);
````



#### Collection Views

Metode tampilan Koleksi memungkinkan Peta dilihat sebagai Koleksi dalam tiga cara berikut:

- `keySet` - Set kunci yang terkandung dalam Peta.
- `values` - Kumpulan nilai yang terkandung dalam Peta. Koleksi ini bukan Set, karena beberapa kunci dapat memetakan ke nilai yang sama.
- `entrySet`- Set pasangan nilai kunci yang terkandung dalam Peta. Antarmuka Peta menyediakan antarmuka bersarang kecil yang disebut Map.Entry, jenis elemen dalam Set ini.



### Pengurutan Object

list l dapat disortir sebagai berikut.

Collections.sort (l);
Jika list terdiri dari elemen String, itu akan diurutkan ke dalam urutan abjad. Jika terdiri dari elemen Tanggal, itu akan diurutkan ke dalam urutan kronologis. Bagaimana ini bisa terjadi? String dan Date keduanya mengimplementasikan antarmuka Sebanding. Implementasi yang sebanding memberikan pemesanan alami untuk kelas, yang memungkinkan objek kelas itu untuk diurutkan secara otomatis. Tabel berikut merangkum beberapa kelas platform Java yang lebih penting yang mengimplementasikan Comparable.

Contoh program pengurutan obyek di dalam list.

````java
list<Box> list = new ArrayList<>();

list.add(new Box(2));
list.add(new Box(4));
list.add(new Box(8));


comparator<Box> comparator = (Box o1, Box o2)->{
    if(o1.getCapacity() > o2.getCapacity()){
        return 1;
    }else if (o1.getCapacity() < o2.getcapacity()){
        return -1;
        else{
            return 0;
        }
````








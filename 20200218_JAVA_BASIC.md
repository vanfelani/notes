# **Junit**

Junit adalah kerangka uji yang menggunakan anotasi untuk mengidentifikasi metode yang menentukan tes. JUnit adalah proyek sumber terbuka yang diselenggarakan di [Github](https://github.com/junit-team/junit). *Tes* JUnit adalah metode yang terkandung dalam kelas yang hanya digunakan untuk pengujian. Ini disebut *kelas Tes* . Untuk menentukan bahwa metode tertentu adalah metode pengujian, beri anotasi dengan `@Test`anotasi. 

## **Definisi Test Method**

JUnit menggunakan anotasi untuk menandai metode sebagai metode pengujian dan mengkonfigurasinya. Tabel berikut ini memberikan ikhtisar tentang anotasi paling penting di JUnit untuk versi 4.x dan 5.x. Semua penjelasan ini dapat digunakan pada metode.

Tabel Anotasi.

| **JUnit 4**                          | **Deskripsi**                                                |
| ------------------------------------ | ------------------------------------------------------------ |
| import org.junit.*                   | Impor pernyataan untuk menggunakan anotasi berikut.          |
| @Test                                | Mengidentifikasi metode sebagai metode pengujian.            |
| @Before                              | Dilakukan sebelum setiap tes. Ini digunakan untuk  menyiapkan lingkungan pengujian (misalnya, membaca data input,  menginisialisasi kelas). |
| @After                               | Dieksekusi setelah setiap tes. Ini digunakan  untuk membersihkan lingkungan pengujian (misalnya, menghapus data sementara,  mengembalikan default). Ini juga dapat menghemat memori dengan  membersihkan struktur memori yang mahal. |
| @BeforeClass                         | Dilakukan sekali, sebelum dimulainya semua tes. Ini  digunakan untuk melakukan aktivitas intensif waktu, misalnya, untuk terhubung  ke database. Metode yang ditandai dengan anotasi ini perlu  didefinisikan staticuntuk  bekerja dengan JUnit. |
| @AfterClass                          | Dilakukan satu kali, setelah semua tes  selesai. Ini digunakan untuk melakukan kegiatan pembersihan, misalnya,  untuk memutuskan sambungan dari database. Metode yang dijelaskan dengan  penjelasan ini perlu didefinisikan sebagai staticbekerja dengan JUnit. |
| @Ignore atau @Ignore("Why disabled") | Menandai bahwa tes harus dinonaktifkan. Ini  berguna ketika kode yang mendasarinya telah diubah dan test case belum  diadaptasi. Atau jika waktu pelaksanaan tes ini terlalu lama untuk  dimasukkan. Ini adalah praktik terbaik untuk memberikan deskripsi  opsional, mengapa tes dinonaktifkan. |
| @Test (expected = Exception.class)   | Gagal jika metode ini tidak melempar pengecualian yang  disebutkan. |
| @Test(timeout=100)                   | Gagal jika metode ini membutuhkan waktu lebih dari 100  milidetik |

### JUnit Parameterized test

JUnit memungkinkan Anda untuk menggunakan parameter di kelas tes. Kelas ini dapat berisi **satu** metode pengujian dan metode ini dijalankan dengan berbagai parameter yang disediakan.

Anda menandai kelas uji sebagai tes parameter dengan `@RunWith(Parameterized.class)`anotasi.

Kelas uji seperti itu harus mengandung metode statis yang dianotasi dengan `@Parameters`anotasi. Metode itu menghasilkan dan mengembalikan koleksi array. Setiap item dalam koleksi ini digunakan sebagai parameter untuk metode pengujian.

Anda dapat menggunakan `@Parameter`anotasi pada bidang publik untuk mendapatkan nilai tes yang disuntikkan dalam tes.

Kode berikut menunjukkan contoh untuk pengujian parameter. Ini menguji `multiply()`metode `MyClass`kelas yang dimasukkan sebagai kelas dalam untuk tujuan contoh ini.

![](C:\Users\NB01\Downloads\2.png)

#### Migration to the Java 8

Library date di Java yang lama yang disediakan oleh JDK hanya mencakup tiga kelas yaitu: *java.util.Date, java.util.Calendar* dan *java.util.Timezone* . 

Ini hanya cocok untuk tugas paling dasar. Untuk apa pun yang bahkan jauh dari rumit, pengembang harus menggunakan perpustakaan pihak ketiga atau menulis banyak kode khusus.

Dan Java 8 memperkenalkan Date Time API yang benar - benar baru  ( *java.util.time. ** ) Yang secara longgar didasarkan pada perpustakaan Java populer yang disebut JodaTime. API baru ini secara dramatis menyederhanakan pemrosesan tanggal dan waktu dan memperbaiki banyak kekurangan dari perpustakaan tanggal yang lama.

### **Fleksibilitas API**

Keuntungan lain adalah fleksibilitas, kerja dengan banyak representasi waktu. 

Pustaka tanggal yang lama hanya menyertakan satu kelas representasi waktu - *java.util.Date* , yang meskipun namanya sebenarnya adalah stempel waktu. Itu hanya menyimpan jumlah milidetik yang berlalu sejak zaman Unix.

API baru memiliki banyak representasi waktu yang berbeda, masing-masing cocok untuk berbagai kasus penggunaan:

- *Instan* - mewakili titik waktu (cap waktu)

- *LocalDate* - mewakili tanggal (tahun, bulan, hari)

- *LocalDateTime* - sama dengan *LocalDate* , tetapi termasuk waktu dengan ketepatan nanosecond

- *OffsetDateTime* - sama dengan *LocalDateTime* , tetapi dengan offset zona waktu

- *LocalTime* - waktu dengan presisi nanosecond dan tanpa informasi tanggal

- *ZonedDateTime* - sama dengan *OffsetDateTime* , tetapi termasuk ID zona waktu

- *OffsetLocalTime* - sama dengan *LocalTime* , tetapi dengan offset zona waktu

- *MonthDay* - bulan dan hari, tanpa tahun atau waktu

- *YearMonth* - bulan dan tahun, tanpa hari atau waktu

- *Durasi* - jumlah waktu direpresentasikan dalam detik, menit dan jam. Memiliki ketepatan nanosecond

- *Periode* - jumlah waktu yang direpresentasikan dalam hari, bulan, dan tahun

  ##### Contoh perbedaan java lama dan java 8

  Dapatkan waktu saat ini

  ```java
  // Old``
  Date now = ``new` `Date();`
  // New`
  ZonedDateTime now = ZonedDateTime.now();
  ```

  Spesifik waktu tertentu

  ```java
  // Old``
  Date birthDay = ``new` `GregorianCalendar(``1990``, Calendar.DECEMBER, ``15``).getTime();` `
  // New``
  LocalDate birthDay = LocalDate.of(``1990``, Month.DECEMBER, ``15``);
  ```

  Ekstraksi bidang tertentu

  ```java
  // Old
  int` `month = ``new` `GregorianCalendar().get(Calendar.MONTH);
  ```

  ```java
  // New
  Month month = LocalDateTime.now().getMonth();
  ```

  Menambah dan Mengurangi waktu

  ```java
  // Old
  GregorianCalendar calendar = ``new` `GregorianCalendar();
  calendar.add(Calendar.HOUR_OF_DAY, -``5``);
  Date fiveHoursBefore = calendar.getTime();
  ```

  ```java
  // New
  LocalDateTime fiveHoursBefore = LocalDateTime.now().minusHours(``5``);
  ```

  Mengubah Waktu Tertentu

  ```java
  // Old
  GregorianCalendar calendar = ``new` `GregorianCalendar();
  calendar.set(Calendar.MONTH, Calendar.JUNE);
  Date inJune = calendar.getTime();
  ```

  ```java
  // New
  LocalDateTime inJune = LocalDateTime.now().withMonth(Month.JUNE.getValue());
  ```

  Memotong

  Memotong mengatur ulang semua bidang waktu lebih kecil dari bidang yang ditentukan. Dalam contoh di bawah ini, semua yang ada di bawah ini akan disetel ke nol.

  ```java
  // Old
  Calendar now = Calendar.getInstance();
  now.set(Calendar.MINUTE, ``0``);
  now.set(Calendar.SECOND, ``0``);
  now.set(Calendar.MILLISECOND, ``0``);
  Date truncated = now.getTime();
  ```

  ```java
  // New
  LocalTime truncated = LocalTime.now().truncatedTo(ChronoUnit.HOURS);
  ```

  Format Waktu dan Parsing

  DateTimeFormatter adalah pengganti SimpleDateFormat lama yang aman untuk thread dan menyediakan fungsionalitas tambahan.

  ```java
  // Old
  SimpleDateFormat dateFormat = ``new` `SimpleDateFormat(``"yyyy-MM-dd"``);
  Date now = ``new` `Date();
  String formattedDate = dateFormat.format(now);
  Date parsedDate = dateFormat.parse(formattedDate);
  ```

  ```java
  // New
  LocalDate now = LocalDate.now();
  DateTimeFormatter formatter = DateTimeFormatter.ofPattern(``"yyyy-MM-dd"``);
  String formattedDate = now.format(formatter);
  LocalDate parsedDate = LocalDate.parse(formattedDate, formatter);
  ```

  ###### BigDecimal

  `BigDecimal`terdiri dari *nilai unscaled* integer arbitrary presisi dan *skala* integer 32-bit . Jika nol atau positif, skala adalah jumlah digit di sebelah kanan titik desimal. Jika negatif, nilai unscaled dari angka dikalikan sepuluh dengan kekuatan negasi skala. Nilai angka yang diwakili oleh `BigDecimal`karenanya `(unscaledValue × 10 -scale )` .

  Timbangan yang dipilih untuk hasil operasi aritmatik

  | Operation | Scale                                     |
  | --------- | ----------------------------------------- |
  | Add       | max(addend.scale(), augend.scale())       |
  | Substract | max(minuend.scale(), subtrahend.scale())  |
  | Multiply  | multiplier.scale() + multiplicand.scale() |
  | Divide    | dividend.scale() - divisor.scale()        |

###### GIT

`git fetch` digunakan untuk melihat update terbaru dari repository, dan sebaiknya dilakukan sebelum `git pull`

```nginx
git fetch [<options>] [<repository> [<refspec> ...]]
git fetch [<options>] <group>
git fetch --beberapa [<options>] [(<repository> | <group>).. ]
git fetch --all [<options>]
```

`git amend` digunakan untuk mengganti komentar di local repository

`git reset head^` digunakan untuk delete commit terakhir di local repository

`git reset` untuk atur ulang HEAD saat ini ke keadaan tertentu.

```nginx
git reset [-q] [<tree-ish>] [--] <pathspec>…
git reset [-q] [--pathspec-from-file=<file> [--pathspec-file-nul]] [<tree-ish>]
git reset (--patch | -p) [<tree-ish>] [--] [<pathspec>…]
git reset [--soft | --mixed [-N] | --hard | --merge | --keep] [-q] [<commit>]
```

`git merge` digunakan untuk menggabungkan dua atau lebih histori pengembangan

```nginx
git merge [-n] [--stat] [--no-commit] [--squash] [--[no-]edit]
	[--no-verify] [-s <strategy>] [-X <strategy-option>] [-S[<keyid>]]
	[--[no-]allow-unrelated-histories]
	[--[no-]rerere-autoupdate] [-m <msg>] [-F <file>] [<commit>…]
git merge (--continue | --abort | --quit)
```

`git stash` digunakan untuk menyimpan perubahan dalam direktori kerja yang kotor

```nginx
git stash list [<options>]
git stash show [<options>] [<stash>]
git stash drop [-q|--quiet] [<stash>]
git stash ( pop | apply ) [--index] [-q|--quiet] [<stash>]
git stash branch <branchname> [<stash>]
git stash [push [-p|--patch] [-k|--[no-]keep-index] [-q|--quiet]
	     [-u|--include-untracked] [-a|--all] [-m|--message <message>]
	     [--] [<pathspec>…]]
git stash clear
git stash create [<message>]
git stash store [-m|--message <message>] [-q|--quiet] <commit>
```

`git cherry pick`digunakan untuk melakukan merge by commit yang ingin Anda merge-kan.

`git push force` digunakan untuk push paksa

`git rebase`
**Anotasi atau '@' dalam SpringBoot**

**@Bean** 
Untuk menandai pemetaan sebuah methode, supaya bisa memiliki bean harus dikasi configurasion fuction ( untuk mengembalikan data)

**@Qualifier**

Agar data tidak duplicat dan harus menambahkan @primary untuk menambahkan data utama yang akan ditampilkan 

**@Autowired** 

Anotasi yang digunakan untuk melakukan inject instance dari suatu bean ke objek yang memiliki dependency Mendetekti tipe yang sama dan nama variabel tidak terpengaruh (membaca tipe bukan membaca variabel name)

**@Entity**

Berguna untuk menandai bahwa kelas tersebut adalah sebuah kelas entity/entitas

**@Id** 
Untuk menandakan bahwa property yang diberikan @Id sebagai primary key

**@Column**

Untuk membuat kolom dari property tersebut dan memberikan nilai unique dan not null

**@Table**
Digunakan untuk membuat table baru

**@Controller**

Menandai bahwa class adalah sebuah controller 

@**PathVariable**

Digunakan untuk mengambil nilai dari URL

**@RequestBody**

Memetakan Badan HttpRequest ke object transfer atau domain

-

**3 Komponen Spring :**

1. Controller, Perantara antara model dan view, yang nantinya view akan mengolah model itu sendiri
2. Service,  Menandakan bahwa class terbsebut sebagai penyedia beberapa fungsi 
3. Repository, Repository digunakan untuk mengakses data dari database



**Model Mapper**

ModelMapper untuk menyederhanakan pemetaan objek, dengan menentukan bagaimana objek memetakan satu sama lain berdasarkan konvensi

Pom.xml untuk menambahkan Modelmapper

```
<dependency>
  <groupId>org.modelmapper</groupId>
  <artifactId>modelmapper</artifactId>
  <version>2.3.0</version>
</dependency>
```

**JSON** 

singkatan untuk **JavaScript Object Notation** — adalah format pertukaran data yang ringan, mudah dibaca dan ditulis oleh manusia, serta mudah diterjemahkan dan dibuat (*generate*) oleh komputer.

## Sintaks dan Struktur

Sebuah objek JSON adalah format data key-value yang biasanya di render di dalam kurung kurawal.

Sebuah objek JSON terlihat seperti berikut ini:

```
{
  "first_name"	: "Sammy",
  "last_name"	: "Shark",
 	
}
```

Fitur format json

@jsonignore

Untuk menyembunyikan field yang tidak ingin ditampilkan kepada user

@jsonformat

Anotasi tujuan umum yang dapat digunakan untuk membuat serial jenis tertentu ke dalam format tertentu.
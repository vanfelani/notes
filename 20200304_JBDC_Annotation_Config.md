**JDBC API**

JDBC API adalah Java API yang dapat mengakses segala jenis data tabular, terutama data yang disimpan dalam Database Relasional.

JDBC membantu Anda menulis aplikasi Java yang mengelola tiga aktivitas pemrograman ini:

Sambungkan ke sumber data, seperti basis data
Kirim pertanyaan dan perbarui pernyataan ke database
Ambil dan proseskan hasil yang diterima dari database sebagai jawaban atas permintaan Anda
Fragmen kode sederhana berikut memberikan contoh sederhana dari tiga langkah ini

```java
public void connectToAndQueryDatabase(String username, String password) {

    Connection con = DriverManager.getConnection(
                         "jdbc:myDriver:myDatabase",
                         username,
                         password);

    Statement stmt = con.createStatement();
    ResultSet rs = stmt.executeQuery("SELECT a, b, c FROM Table1");

    while (rs.next()) {
        int x = rs.getInt("a");
        String s = rs.getString("b");
        float f = rs.getFloat("c");
    }
}
```

sintaks pendek diatas adalah instantiates objek DriverManager untuk terhubung ke driver database dan login ke database, instantiates objek Pernyataan yang membawa permintaan bahasa SQL Anda ke database; instantiates objek ResultSet yang mengambil hasil kueri Anda, dan mengeksekusi loop sederhana, yang mengambil dan menampilkan hasil tersebut. 



**CRITERIA BUILDER DAN CRITERIA QUERY**

``CriteriaBuilder nama_variable = builder.createCriteriaDelete``

CriteriaBuilder berfungsi sebagai pembuat criteria dimana criteria tersebut digunakan untuk membuat sebuah function yang akan digunakan, criteria dapat menggunakan 3 class yaitu CriteriaDelete, CriteriaUpdate dan CriteriaQuery(digunakan untuk query yang kompleks lalu kita coding alur logic mirip dengan sql query), kalau ingin menggunakan transaction kita harus memulai dengan mendeklarasikan EntityTransaction nama_variable = entityManager.getTransaction

Contoh memulai criteria 
``CriteriaBuilder builder = entityManager.getCriteriaBuilder();`
`CriteriaQuery<nama_class> criteria = builder.createQuery(nama_class.class); `

lalu select class menggunakan

`Root<namaclass> rootNamaClass = criteria.from(namaClass.Class);`

	criteria.select/where/multiselect(builder.sum/



***Annotation***

Spesifikasi JPA mendukung 4 strategi pembuatan kunci primer berbeda yang menghasilkan nilai kunci primer secara terprogram atau menggunakan fitur basis data, seperti kolom atau sekuens yang ditambahkan secara otomatis. Satu-satunya yang harus Anda lakukan adalah menambahkan anotasi @GeneratedValue ke atribut kunci utama Anda dan memilih strategi generasi.

### *GenerationType.AUTO*

adalah tipe generasi default dan memungkinkan penyedia ketekunan memilih strategi pembuatan.



```java
@Id
@GeneratedValue(strategy = GenerationType.AUTO)
@Column(name = "id", updatable = false, nullable = false)
private Long id;
```



Jika Anda menggunakan Hibernate sebagai penyedia , ia memilih strategi pembuatan berdasarkan dialek khusus basis data. Untuk kebanyakan database populer, ia memilih * GenerationType.SEQUENCE * yang akan saya jelaskan nanti.

### GenerationType.IDENTITY

GenerationType.IDENTITY * adalah yang termudah untuk digunakan tetapi bukan yang terbaik dari sudut pandang kinerja. Itu bergantung pada kolom basis data yang ditambahkan secara otomatis dan memungkinkan basis data menghasilkan nilai baru dengan setiap operasi penyisipan. Dari sudut pandang basis data, ini sangat efisien karena kolom peningkatan otomatis sangat dioptimalkan, dan tidak memerlukan pernyataan tambahan apa pun.

```java
@Id
@GeneratedValue(strategy = GenerationType.IDENTITY)
@Column(name = "id", updatable = false, nullable = false)
private Long id;
```

```java
@Id
@GeneratedValue(strategy = GenerationType.IDENTITY)
private PK id;
```

Pendekatan ini memiliki kelemahan signifikan jika Anda menggunakan Hibernate. Hibernate memerlukan nilai kunci utama untuk setiap entitas yang dikelola dan oleh karena itu harus segera melakukan pernyataan penyisipan. Ini mencegahnya dari menggunakan [teknik optimasi yang berbeda] seperti batch JDBC. 

**Annotation Prepersist Dan Pre Update**

Metode callback yang sama atau metode pendengar entitas dapat dijelaskan dengan lebih dari satu penjelasan panggilan balik. Untuk entitas tertentu, Anda tidak dapat memiliki dua metode yang dianotasi oleh anotasi panggilan balik yang sama apakah itu metode panggilan balik atau metode pendengar entitas. Metode panggilan balik adalah metode tanpa arg tanpa jenis pengembalian dan nama arbitrer apa pun. Seorang pendengar entitas memiliki tanda tangan `void (Objek) 'di mana Objek tersebut dari tipe entitas yang sebenarnya (perhatikan bahwa Hibernate Entity Manager mengendurkan kendala ini dan memungkinkan` Objek` dari `java.lang. Jenis tipe objek (berbagi pembagian pendengar di seluruh beberapa entitas.)

Metode panggilan balik dapat meningkatkan `RuntimeException`. Transaksi saat ini, jika ada, harus dibatalkan. Callback berikut didefinisikan:

@PrePersist Dieksekusi sebelum operasi entitas bertahan sebenarnya dieksekusi atau di-cascade. Panggilan ini sinkron dengan operasi yang bertahan.

@PreUpdate Dieksekusi sebelum database di Update

Contoh sintaks menggunakan Prepersist dan Preupdate

```java
@PrePersist
public void prePersist(){
    createdDate = LocalDateTime.now();
}

@PreUpdate
public void preUpdate(){
    modifiedDate = LocalDateTime.now();
}
```

**HIBERNATE - CONFIG**

`**hibernate.hbm2ddl.auto**` (e.g. `none` (default value), `create-only`, `drop`, `create`, `create-drop`, `validate`, and `update`)

Diatur dari `SchemaManagementTool`salah satu bagian dari `SessionFactory` lifecycle. salah satu penggunaan yang valid adalah `externalHbm2ddlName` nilai dari penggunaan tersebut adalah enum:

- `none`

  Tidak ada aksi yang akan dilakukan.

- `create-only`

  Men- Generate database yang akan dibuat.

- `drop`

  Men- Generate database yang akan dihapus.

- `create`

  Database dropping akan dihasilkan diikuti oleh pembuatan basis data.

- `create-drop`

  Membuat skema dan buat ulang di startup SessionFactory. Selain itu, lepaskan skema pada shutdown SessionFactory.

- `validate`

  Memvalidasi database scema

- `update`

  Update scema database

  

hibernate.hbm2ddl.import_files = schema-generation.sql
 hibernate.hbm2ddl.import_files_sql_extractor = org.hibernate.tool.hbm2ddl.MultipleLinesSqlCommandExtractor

digunakan untuk import file dapat menjadi multiline
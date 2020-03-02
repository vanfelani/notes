# Mockito & Hibernate
***

# ~ Mockito

#### 1. Pengenalan Mockito 
Menurut [Wikipedia](https://en.wikipedia.org/wiki/Mockito) Mockito adalah framework Open-Source Java yang memungkinkan "Test Object-Double" dalam pengujian unit otomatis untuk tujuan Test Driven Development(TDD) atau Behavior Driven Development(BDD).
Mockito berfungsi untuk menguji fungsionalitas kelas secara terpisah. Mockito tidak memerlukan koneksi Database untuk mengetes fungsionalitas kelas.

#### 2. Keuntungan Menggunakan Mockito 

  - **No Handwriting** (Tidak perlu menulis sendiri objek tiruan).
  - **Refactoring Safe** (Mengganti nama method atau merubah parameter tidak akan merusak unit test karena Mockito dibuat saat runtime).
  - **Exception Support** (Mensupport exception).
  - **Order Check Support** (Mensupport untuk mengecek urutan pada panggilan method).
  - **Annotion Support** (Mensupport untuk membuat mocks menggunakan annotasi).

### 3. Macam - macam Annotasi pada Mockito
- **@Mock** : berfungsi untuk me"mock"/ meniru objek yang membantu meminimalisir objek tiruan yang berulang. Itu membuat test kode dan verifikasi error lebih mudah dibaca. Anotasi **@Mock** tersedia dalam package "**org.mockito**".
- **@RunWith** : berfungsi untuk menjaga test tetap bersih dan meningkatkan debugging. **@RunWith** juga bisa mendeteksi potongan kode yg tidak terpakai pada test code dan menginisialisasinya dengan Anotasi **@Mock** . Anotasi **@RunWith** tersedia dalam package "**org.junit.runner**".
- **@InjectMocks** : berfungsi untuk menandai field atau parameter dimana "injeksi" hasrus dilakukan. Anotasi **@InjectMocks** tersedia dalam package "**org.mockito**".
- [dll.](https://www.javatpoint.com/mockito-annotations)

> Contoh penggunaan Annotasi di atas.
~~~
package org.example;

import java.sql.*;
import java.util.List;

import org.junit.*;
import org.junit.runner.RunWith;
import org.mockito.*;
import org.mockito.junit.MockitoJUnitRunner;

import static org.junit.Assert.*;
import static org.mockito.Mockito.*;

import code.id.jdbc.entities.Item;
import code.id.jdbc.repositories.ItemRepo;

@RunWith(MockitoJUnitRunner.class)
public class ItemRepoTest {

    private static final int TEST_ID = 99;
    private static final String TEST_NAME = "Test Item";
    
    @InjectMocks
    private ItemRepo itemRepo;

    @Mock
    private Connection conn;

    @Mock
    private Statement stat;

    @Mock
    private PreparedStatement preStat;

    @Mock
    private ResultSet res;

    @Before
    public void before() throws SQLException {
        when(conn.createStatement()).thenReturn(stat);
        when(conn.prepareStatement(any(String.class))).thenReturn(preStat);
        
        when(stat.executeQuery(any(String.class))).thenReturn(res);

        when(preStat.executeQuery()).thenReturn(res);
        when(preStat.executeUpdate()).thenReturn(1);
    }

    @Test
    public void shouldAdded() throws SQLException {
        Item item = new Item(TEST_ID, TEST_NAME);
        boolean result = itemRepo.add(item);

        assertTrue(result);
    }
~~~
### 4. Install Mockito dengan Maven
- Pertama, pastikan [maven](https://www.baeldung.com/install-maven-on-windows-linux-mac) sudah terpasang pada project anda.
- Lalu terakhir, taruh kode dibawah pada file "pom.xml" (diantara "< dependencies>" ... "</  dependencies>").
~~~
<dependency>
      <groupId>org.mockito</groupId>
      <artifactId>mockito-core</artifactId>
      <version>3.3.0</version>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.13</version>
      <scope>test</scope>
    </dependency>
~~~

# ~ Hibernate

### 1. Pengenalan Hibernate
Hibernate merupakan salah satu framework Object Relational Mapping(ORM) di Java yang menyediakan sebuah template untuk melakukan operasi-operasi data seperti insert, update, delete, dan select. Object Relational Mapping(ORM) adalah sebuah paradigma untuk mengubah model database relational menjadi object oriented programming.

### 2. Install Hibernate dengan Maven
Hanya sedikit konfigurasi yang perlu dilakukan yaitu dialect database dan driver class, tidak perlu compile ulang aplikasi.
- Pertama, pastikan [maven](https://www.baeldung.com/install-maven-on-windows-linux-mac) sudah terpasang pada project anda.
- Lalu taruh kode dibawah pada file "pom.xml" (diantara "< dependencies>" ... "</ dependencies>").
~~~
<dependency>
      <groupId>org.hibernate</groupId>
      <artifactId>hibernate-core</artifactId>
      <version>5.4.12.Final</version>
    </dependency>
~~~
- Kemudian buatlah file "hibernate.properties" yang berisikan kode dibawah dan taruh di "/projectAnda/src/main/resources/".
~~~
hibernate.connection.driver_class = com.mysql.cj.jdbc.Driver
hibernate.connection.url = jdbc:mysql://localhost:3306/nama_db
hibernate.connection.username = user_mysql
hibernate.connection.password = pass_mysql
hibernate.dialect = org.hibernate.dialect.MySQLDialect
~~~
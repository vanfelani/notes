# **JDBC**

## Pengertian.

JDBC merupakan perantara antara Java dengan basis data atau kumpulan interface yang dapat menghubungkan java ke database.



## Memporses statement SQL dengan JDBC.

1. Membuat koneksi
2. Membuat statment
3. Menjalankan query
4. Menampilkan result set
5. menutup koneksi.



### a. membuat koneksi

jalan kan terlebih dulu untuk databse nya.

Sebelum melakukan koneksi tambahkan dependency terlebih dahulu di POM.XML dengan sintaks :

```
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.19</version>
</dependency>
```

jika untuk mengecek zone waktu bisa menggunakan `select @@global.time_zone;`

- lalu buat file config.properties untuk menempatkan macam properties untuk kebutuhan seperti username dbs,  username dbs, dan nama dbs.

contoh : 

```java
database.username = root
database.password = root
database.db = bootcamp
```

lalu masukkan sintak ke pom.xml pada bagian build : 

```java
<resources>
    <resource>
        <directory>$(basedir)/config</directory>
        <excludes>
            <exclude>**</exclude>
        </excludes>
    </resource>
</resources>
```

lalu ketikkan sintaks agar dapat mengakses database : 

```java
import java.io.FileInputStream;
import java.io.InputStream;
import java.sql.*;
import java.util.*;
import Repositories.*;

import javax.sql.DataSource;

public class Application {
    public static DataSource getDataSourceConnection(Properties prop) throws 		SQLException {
        MysqlDataSource ds = new MysqlDataSource();
        ds.setURL("jdbc:mysql://localhost:3306/" + 						               prop.getProperty("database.name"));
        ds.setUser(prop.getProperty("database.user"));
        ds.setPassword(prop.getProperty("database.password"));

        return ds;
    }
    public static void main(String[] args) throws Exception {
         try (InputStream input = new 													FileInputStream("./config/config.properties")) {
            Properties prop = new Properties();
            prop.load(input);

            System.out.println(prop.getProperty("database.user"));
            System.out.println(prop.getProperty("database.password"));

            DataSource ds = getDataSourceConnection(prop);
            Connection conn = ds.getConnection();

            test(conn);
        }
    }
}
```

### b. membuat statement, menjalankan query , dan result set.

buat method dengan contoh add:

untul setiap statement manupulation akan mengembalikan nilai boolean untuk menandakan terjadinya perubahan atau tidak.

```java
public boolean add(Item entity) throws SQLException {
/*ini pembuatan statement yang akan di eksekusi*/
    String sql = "INSERT INTO item (id, name) VALUES (?,?)";
    /*eksekusi query*/
    try (PreparedStatement stmt = conn.prepareStatement(sql)) {
        stmt.setInt(1, entity.getId());
        stmt.setString(2, entity.getName());
        /*mengembalikan resul berupa boolean*/
        int result = stmt.executeUpdate();
        return result == 1;
    }
}
```

### c. menutup koneksi

menutup koneksi dengan sintaks  `conn.close();` 



### D.menjalankan transaction di dengan JDBC.

contoh sintaks :

```
public static void test(Connection conn) throws SQLException {
    ItemRepository itemRepository = new ItemRepository(conn);
    try {
        conn.setAutoCommit(false);
        System.out.println("add: " + itemRepository.add(new Item(11, "Bambang")));
        Item item = itemRepository.findById(11);
        System.out.println("findById: " + item);
        item.setName("Agus");
        System.out.println("Edit: " + itemRepository.edit(item));
        System.out.println("Remove: " + itemRepository.remove(item));

        conn.commit();
    } catch (SQLException e) {
        conn.rollback();
    }
}
```

di sini autocommit disetting false, dikarenakan autocimmit secara default memiliki hasil true.

ketikan conn.commit(); akan auto close connection.



dan disini kita untuk koneksi menggunkan DataSource karena akan menyediakan connection cooling yang akan memanage prioritas ketika di pakai oleh banyak orang dibandingkan DriverManager.
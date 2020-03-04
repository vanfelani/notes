# Hibernate ORM

ORM (Object Relational Mapping) adalah sebuah konsep dimana sebuah objek adalah representasi dari basis data relasional 

class" yang digunakan harus di daftarkan pada hibernate java karena tidak menggunakan spring dengan menggunakanan syntax 

configuration.addAnnotatedClass(<nama_class.class>);

#### Anotasi Pada Hibernate
  - **@Table(name = <nama_table_database>)** untuk menentukan table yang digunakan pada class.
 - **@Entity** digunakan untuk menandakan bahwa class tersebut merupakan sebuah entitas
 - **@Id** digunakan untuk menandakan primary key pada class yang merujuk pada database
 - **@ManyToOne** berguna untuk membangun relasi many to one antar tabel
 - **@JoinColumn** digunakan untuk melakukan join antar tabel


jika ada nama tabel yang berbeda dari variabel pada class, gunakan notasi column
contoh : 
```java
@Column(<nama_field_pada_database>)
         private <tipe_data>  <nama_variabel_java>;
```
SessionFactory : standar bawaan hibernate
EntityManager : standar java yang membungkus session hibernate


#### Contoh Sintaks Untuk Menampilkan Seluruh Data
```java
    public Item findItemById(Integer id) throws SQLException {
        return entityManager.find(Item.class, id);
    }
```

#### Contoh Sintaks Untuk Menampilkan Data Berdasarkan Id
```java
    public Item findItemById(Integer id) throws SQLException {
        return entityManager.find(Item.class, id);
    }
```

#### Contoh Sintaks Untuk Save (Add + Edit)
```java
    public Item save(Item entity) throws SQLException {
        EntityTransaction transaction = entityManager.getTransaction();
        transaction.begin();
        Item result = entityManager.merge(entity);
        transaction.commit();
        return result;
```
#### Contoh Sintaks Untuk Hapus Berdasarkan ID
```java
    public boolean removeById(Integer id) throws SQLException {
        EntityTransaction transaction = entityManager.getTransaction();
        transaction.begin();
        int result = entityManager.createQuery("DELETE FROM Item i WHERE i.id = :id")
                .setParameter("id", id)
                .executeUpdate();
        transaction.commit();
        return result == 1;
    }
```
 

```text
Catatam : nama class dan nama field, tidak ada urusan dengan database
```

annotation adalah metadata untuk field method atau class


#### Criteria


#### kelebihan dari Criteria yaitu :
 1. dapat mendeteksi error saat compile 
 2. query pada criteria didefinisikan oleh instansiasi pada objek java

contoh sintaks criteria : 
```java
SELECT c FROM Country c
```
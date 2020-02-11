## Lambda Expressions

**Lambda** dapat digunakan ketika *anonymous class* hanya memiliki sebuah *method*.

~~~java
printPersons(
    roster,
    (Person p) -> p.getGender() == Person.Sex.MALE
        && p.getAge() >= 18
        && p.getAge() <= 25
);
~~~

Hanya fungsional *Interface* yang bisa dijadikan **Lambda**, ada bawaan dari java untuk fungsional interface yaitu *predicate*.


## Method References

**Lambda Expressions** digunakan ketika ada *anonymous method*. Terkadang, **Lambda Expressions** tidak melakukan apa - apa selain memanggil method yang sudah ada. Karena **Lambda Expressions** hanya memanggil method yang sudah ada, method *reference* bisa digunakan sebagai gantinya. Sebagai contoh : 

~~~java
Arrays.sort(rosterAsArray, Person::compareByAge);
~~~

*Method reference* Person::compareByAge sama dengan **lambda expressions** (a, b) -> Person.compareByAge(a, b).


<h4>Kinds of Method References</h4>


| Kind 	                                                                        |   Example                                 |
| ----                                                                          |   -------                                 |
| Reference to a static method 	                                                |   ContainingClass::staticMethodName       |
| Reference to an instance method of a particular object 	                    |   ContainingObject::instanceMethodName    |
| Reference to an instance method of an arbitrary object of a particular type   | 	ContainingType::methodName              |
| Reference to a constructor  	                                                |   ClassName::new                          |

## When to Use Nested Classes, Local Classes, Anonymous Classes, and Lambda Expressions

**Lambda Expressions** digunakan untuk situasi yang lebih spesifik :
1. **Local class**: digunakan ketika memerlukan class yang di pakai berkali-kali. Namun, pada implementasinya tidak direkomendasikan.
2. **Anonymous class**: digunakan ketika memerlukan satu atribut atau method tambahan ].
3. **Lamda expressions**: digunakan ketika membutuhkan *instance* sederhana dari *fungtional interface*
4. **Nested class**: digunakan ketika akan membuat class menjadi lebih luas.

## Enum Types
**Enum types** adalah sebuah data tipe yang membolehkan variabel di set secara konstan. Variabel harus sama dengan satu nilai set yang sudah ditentukan sebelumnya.

contoh penggunaan **enum**:
~~~java
public enum Gender{
	MALE = ('M');
	FEMALE = ('F");
	
	private static final char value;
	
	private Gender(char value){
		this.value = value;
	}
}
~~~

contoh pemanggilan pada method *main*:
~~~java
public static void String main(String[] args) {
	for (Gender value : Gender.value()){
		System.out.println(value);
	}	
}
~~~

## Annotations
**Annotations** digunakan sebagai informasi tambahan yang bisa ditambahkan di class, variabel atau method. Beberapa kegunaan untuk annotations:
1. **Information for the compiler**: Annotations dapat digunakan oleh compiler untuk mendeteksi kesalahan atau menekan peringatan.
2. **Compile-time and deployment-time processing**: *Software Tools* yang dapat memproses informasi Annotations untuk menghasilkan *code, XML files* dan sebagainya.
3. **Runtime processing**:  bebeapa annotations tersedia untuk diperiksa ketika runtime.

<h4>The Format of an Annotation</h4>

Beberapa format pada annotation: @Entity, @Overide, @SuppressWarnings.

**Where Annotations Can Be Used**
Annotations bisa diterapkan ke deklarasi: deklarasi *class*, *fields*, *methods*, dan program lainnya. Ketika digunakan pada suatu deklarasi, setiap annotations sering muncul berdasarkan konvensi pada barisnya sendiri.

## Predefined Annotation Types
<h4>Annotation Types Used by the Java Language</h4>
1. **@Deprecated**: annotations menunjukkan bahwa  elemen yang ditandai sudah usang dan seharusnya tidak lagi digunakan. Kompiler menghasilkan peringatan setiap kali suatu program menggunakan metode, kelas, atau bidang dengan anotasi @Deprecated
2. **@Override**: annotations memberi tahu  kompiler bahwa elemen dimaksudkan untuk menimpa elemen yang dideklarasikan dalam superclass.
3. **SuppressWarnings**: annotation memberitahu kompiler untuk menekan peringatan spesifik yang akan dihasilkannya.

<h4>Annotations That Apply to Other Annotations</h4>
1 **@Retention**: annotations menentukan bagaimana anotasi yang ditandai disimpan.
2. **@Documented**: annotations menunjukkan bahwa setiap kali anotasi yang ditentukan digunakan, elemen-elemen tersebut harus didokumentasikan menggunakan Javadoc.
3. **@Target**: annotations menandai anotasi lain untuk membatasi elemen Java apa saja yang dapat diterapkan anntations.

## Interface

**Interface** digunakan ketika situasi diantara kelompok programmer yang memerlukan standart(kontrak) untuk menentukan bagaimana *software* saling berinteraksi. Pada **Java Programming**, interface adalah *reference type*, sama dengan class yang hanya berisi konstanta, *static method* dan *nested types*.

<h4>Implementing an Interface</h4>
Ketika mengimplementasikan interface, ada beberapa hal yang harus diperhatikan:
1. class pada interface tidak bisa punya variabel(hanya variabel static atau konstan)
2. semua method pada interface pasti *public abstrack*
3. ketika akan menggunakan class interface, harus dengan tambahan *implements* pada class yang akan menggunakan class interface
4. classs yang memakai class interface harus mengimplementasikan method yang ada pada class interface

contoh implementasi interface, class interface Shapeable

~~~java
public interface Shapeable {

    public abstract double perimeter();
    public abstract double area();
    
}
~~~

class Rectangle :

~~~java
public class Rectangle implements Shapeable{
    private double width;
    private double height;

    public Rectangle (double width,double height){
        this.width=width;
        this.height=height;
    }

    public double getHeight() {
        return this.height;
    }

    public void setHeight(double height) {
        this.height = height;
    }

    public double getWidth() {
        return this.width;
    }

    public void setWidth(double width) {
        this.width = width;
    }

    @Override
    public double perimeter(){
        return 2 * (width*height);
    }

    @Override
    public double area(){
        return width*height;
    }

    @Override
    public String toString(){
        return String.format("%s (width: %.2f, heigth: %.2f)", getClass().getSimpleName(), width, height);
    }

}
~~~

class Square:
~~~java
public class Square implements Shapeable{

    private double side;

    public Square(double side) {
        this.side = side;
    }

    public double getSide() {
        return this.side;
    }

    public void setSide(double side) {
        this.side = side;
    }

    @Override
    public double perimeter(){
        return 4 * side;
    }

    @Override
    public double area(){
        return side * side;
    }

    @Override
    public String toString(){
        return String.format("%s (Side: %.2f)", getClass().getSimpleName(),side);
    }

}
~~~

Pemanggilan pada main method:
~~~java
public class Application {

    @SuppressWarnings("deprecation")
    public static void main(String[] args) {
        Shapeable[] shapeables = {
                new Rectangle(2,4),
                new Square(2)
        };

        for(Shapeable shapeable : shapeables){
            System.out.printf("%s (Perimeter: %.2f, Area %.2f)\n", shapeable, shapeable.perimeter(), shapeable.area());
        }
    }
    
}
~~~
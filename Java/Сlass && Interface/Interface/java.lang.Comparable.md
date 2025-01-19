[[Лекция - Comparator и Comparable в Java]]
В Java интерфейсы `Comparable` и `Comparator` используются для реализации сравнения объектов. **==Они позволяют сортировать объекты по определённому критерию==**. (см. [[java.util.Comparator]])
### Рассмотрим их подробнее `Comparable`
`Comparable` используется для ==определения естественного порядка== сортировки объектов. Этот порядок обычно является "**по умолчанию**" для класса.
#### Основное:
- Используется для естественной сортировки объектов.
- Сортировка определяется самим объектом, который реализует интерфейс.
- Метод: `compareTo(T o)` — **это единственный метод интерфейса** `Comparable` в Java, который используется для определения "естественного порядка" объектов. Он позволяет сравнивать текущий объект (`this`) с другим объектом (`o`) одного и того же типа `T`.
#### Методы:
- `public int compareTo(T o);` - Cравнивает текущий объект (`this`) с другим объектом (`o`) одного и того же типа `T`, **==возвращает целое число:==** (**`< 0`** / **`0`** / **`> 0`**) = текущий объект (**меньше** / **равен** / **больше** переданного) [^1]


<dir style="
    width: 100%; 
    border-collapse: collapse; 
    font-family: Arial, sans-serif; 
    font-size: 15px; 
    text-align: left; 
    margin: 20px 5px; 
    padding: 5px 5px; 
    background-color: rgba(255, 165, 0, 0.3);
    border-radius: 8px; 
    overflow: hidden; 
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
	border: 1px solid #d6d8db;
">
<span style="font-size: 1.2em; font-weight: bold; margin: 0; line-height: 1.2; display: inline-block; margin-bottom: 10px;">Важно</span><br>
У класса <code>String</code> есть так же метод <code>compareToIgnoreCase()</code> который проверяет две строки на равенство, <b>без</b> учета регистра (<b>именно у класса</b> <code>String</code>)<br>
Метод <code>compareTo()</code> реализован у многих классов, соответсвенно у многих членов классов можно вызвать данный метод.
</dir> 

***Пример c*** `compareToIgnoreCase()` [^8]
***Другие методы у которых реализован*** `compareTo()` [^9]


<table class="language-java_td" style="width: 99%; border-collapse: collapse; margin-bottom: 5px;">
    <tr>
        <strong style="font-size: 1.1em; color: #333;">Пример 1:</strong>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333;"><span style="border: 1px solid black; padding: 2px;">#1</span>
&nbsp; У нас есть класс `Person`, где мы хотим сравнивать людей по имени:</strong>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333;"><span style="border: 1px solid black; padding: 2px;">#2</span>
&nbsp; У нас есть класс `Student`, где мы хотим сравнивать людей по возврасту:</strong>
        </td>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre class="language-java_td" style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
                <code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
import java.util.Arrays;  
 
public class Person implements Comparable＜Person＞ {  
    String name;  
     
    public Person(String name) {  
        this.name = name;  
    }  
     
    @Override  
    public String toString() {  
        return '{' + name + '}';  
    }  
      
    @Override  
    public int compareTo(Person o) {  // Выполняется сравнение строковых полей `name` двух объектов `Person`
🟠      return this.name.compareTo(o.name);  
    }  
   
}  
  
class Main {  
    public static void main(String[] args) {  
        Person[] names = {new Person("Alice"), new Person("Charlie"), new Person("Bob")};  
        Arrays.sort(names); // Вызовет compareTo у String  
        System.out.println(Arrays.toString(names));  
    }  
}
                </code>
            </pre>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
                <code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
import java.util.ArrayList;  
import java.util.Collections;  
 
public class Student implements Comparable＜Student＞ {  
    private int age;  
      
    public Student(int age) {  
        this.age = age;  
    }  
      
    @Override  
    public String toString() {  
        return "{" + age + "}";  
    }  
      
    @Override  
    public int compareTo(Student other) {  // Сортировка по возрасту  
🔴      return this.age - other.age; 
    }  
}  
  
class Main {  
    public static void main(String[] args) {  
        ArrayList＜Student＞ people = new ArrayList＜＞();  
        people.add(new Student(12));  
        people.add(new Student(23));  
        people.add(new Student(43));  
        
        Collections.sort(people); // Используется compareTo()  
        System.out.println(people); // Вывод: [Alice, Bob, Charlie]  
    }  
}
                </code>
            </pre>
        </td>
    </tr>
</table>


###### Подробнее<span style="border: 1px solid black; padding: 2px; line-height: 1.75;">#1</span>:<br/>
 &nbsp;🟠 - Метод `compareTo` у класса `String` в Java реализует лексикографическое сравнение строк. [[Метод `compareTo` у класса `String`]]
 
 ###### Подробнее<span style="border: 1px solid black; padding: 2px; line-height: 1.75;">#2</span>:<br/>
 &nbsp;🔴 - Метод `compareTo` который мы обязаны реализовать имплементировав интерфейс `Comparable`, возвращает `return this.age - other.age;`. Логика метода реализована в соотвествии с контрактом [^6]


***Вот версия кода без использования дженериков: [^5]***

#### Где используется `compareTo(T o)`
Метод `compareTo` из интерфейса **`Comparable`** используется во многих частях стандартной библиотеки Java, а также в пользовательском коде, когда требуется сравнение объектов для **сортировки** или **поиска**

> ***Например:***
> 1. **Сортировке** (`Arrays.sort`, `Collections.sort`, `Stream.sorted()`)
>   - `Arrays.sort`:
>   ```java
>   Arrays.sort(array); // Сортирует массив объектов, реализующих Comparable
>   ```
>   - `Collections.sort`:
>   ```java
>   List＜String＞ list = Arrays.asList("Charlie", "Alice", "Bob");
>   Collections.sort(list); // Сортирует список
>   ```
>   - `Stream.sorted()`:
>   ```java
>   list.stream().sorted().forEach(System.out::println); // Потоковая сортировка
>   ```
>   
> 2. **Поиске** (`Collections.binarySearch`, `Arrays.binarySearch`).
>   - `Arrays.binarySearch`:
>   ```java
>   int index = Arrays.binarySearch(array, key); // Поиск индекса элемента
>   ```
>   - `Collections.binarySearch`:
>   ```java
>   int index = Collections.binarySearch(list, key);
>   ```
> 
> 3. **Коллекциях с естественным порядком**:
>     - `TreeSet` и `TreeMap`:
>   ```java
>   TreeSet＜Person＞ set = new TreeSet＜＞();
>   set.add(new Person("Alice"));
>   set.add(new Person("Bob"));
>   ```
>   - `PriorityQueue`:
>   ```java
>   PriorityQueue＜Person＞ queue = new PriorityQueue＜＞();
>   queue.add(new Person("Charlie"));
>   ```
> 
> 4. **Поиск минимальных/максимальных значений: **(`Collections.min`, `Collections.max`):
>   ```java
>   Person min = Collections.min(list);
>   Person max = Collections.max(list);
>   ```
>   
> 5. **Потоковые данные (Stream API):**
>   ```java
>   Optional＜Person＞ minPerson = list.stream().min(Comparator.naturalOrder());
>   Optional＜Person＞ maxPerson = list.stream().max(Comparator.naturalOrder());
>   ```
<dir style="
    width: 100%; 
    border-collapse: collapse; 
    font-family: Arial, sans-serif; 
    font-size: 15px; 
    text-align: left; 
    margin: 20px 5px; 
    padding: 5px 5px; 
    background-color: rgba(255, 165, 0, 0.3);
    border-radius: 8px; 
    overflow: hidden; 
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
	border: 1px solid #d6d8db;
">
<code>compareTo</code> обеспечивает <strong>"естественный порядок"</strong> объектов и широко применяется во всех стандартных механизмах сортировки и поиска в Java.
</dir>

<table class="language-java_td" style="width: 99%; border-collapse: collapse; margin-bottom: 5px;">
	<tr>
		<strong style="font-size: 1.1em; color: #333;">Общий пример:</strong>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333;"><span style="border: 1px solid black; padding: 2px;">#1</span>
&nbsp; У нас есть класс `Person`, где мы хотим сравнивать людей по имени (Общий пример):</strong>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333;"><span style="border: 1px solid black; padding: 2px;">#2</span>
&nbsp; У нас есть класс `Student`, где мы хотим сравнивать людей по возврасту:</strong>
        </td>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre class="language-java_td" style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
import java.util.*;
 
class Student implements Comparable＜Student＞ {
    private String name;
    private int age;
 
    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
 
    // Comparable: сортировка по возрасту
    @Override
❗️  public int compareTo(Student other) { // Определения естественного порядка
        return this.age - other.age;
    }
 
    public String getName() {
        return name;
    }
 
    public int getAge() {
        return age;
    }
}
 
🟤class StudentNameComparator implements Comparator＜Student＞ {
    @Override
    public int compare(Student s1, Student s2) {
        return s1.getName().compareTo(s2.getName());
    }
 }
 
public class Main {
    public static void main(String[] args) {
        List＜Student＞ students = new ArrayList＜＞();
        students.add(new Student("Alice", 23));
        students.add(new Student("Bob", 20));
        students.add(new Student("Charlie", 21));
 
        // Comparable: сортировка по возрасту
🔴      Collections.sort(students);
        System.out.println("Сортировка по возрасту:");
        for (Student student : students) {
            System.out.println(student.getName() + " - " + student.getAge());
        }
 
        // Comparator: сортировка по имени
🔴      Collections.sort(students, new StudentNameComparator());
        System.out.println("\nСортировка по имени:");
        for (Student student : students) {
            System.out.println(student.getName() + " - " + student.getAge());
        }
    }
}
				</code>
            </pre>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
import java.util.Arrays;  
 
public class Student implements Comparable＜Student＞ {  
    private int age;  
 
    public Student(int age) {  
        this.age = age;  
    }  
 
    @Override  
    public String toString() {  
        return "{" + age + "}";  
    }  
 
    @Override  
    public int compareTo(Student other) {  
        return this.age - other.age; // Сортировка по возрасту  
    }  
}  
 
class Main {  
    public static void main(String[] args) {  
        // Создаем массив студентов
        Student[] people = new Student[3];  
        people[0] = new Student(12);  
        people[1] = new Student(23);  
        people[2] = new Student(43);  
 
        // Сортируем массив
🔴        Arrays.sort(people); // Используется compareTo()  
 
        // Выводим результат
        System.out.println(Arrays.toString(people)); // Вывод: [{12}, {23}, {43}]
    }  
}
				</code>
            </pre>
        </td>
    </tr>
</table>

###### Подробнее <span style="border: 1px solid black; padding: 2px; line-height: 1.75;">#1</span>:<br/>
 🔴 - Статический метод `sort()` класса `Collections` в Java предоставляет удобный способ ==**сортировки списков объектов**==. Этот метод используется для упорядочивания **элементов списка** согласно естественному порядку (если элементы реализуют интерфейс `Comparable`) или с использованием внешнего компаратора (интерфейса `Comparator`). [[Collections.sort()]]
 🟤 - Этот код **реализует пользовательский порядок с помощью компаратора** для класса `Student`. [^7]
 
###### Подробнее <span style="border: 1px solid black; padding: 2px; line-height: 1.75;">#2</span>:<br/>
 🔴 - Статический метод `sort()` класса `Arrays` **==для сортировки массивов==** примитивных типов и объектов. Этот метод используется для упорядочивания **элементов массива** согласно естественному порядку (если элементы реализуют интерфейс `Comparable`) или с использованием внешнего компаратора (интерфейса `Comparator`). [[Arrays.sort()]]


![[Снимок экрана 2024-12-21 в 18.31.06.png|850]]


![[Снимок экрана 2024-12-19 в 20.54.01.png|700]]

















[^3]:##### Метод `compareTo` у класса `String`
    Он определён как:
    ```java
    public int compareTo(String anotherString)
    ```
    ##### Как работает `compareTo` у `String`:
    1. **Возвращаемое значение**:
        - **Отрицательное значение**: Если текущая строка лексикографически меньше строки `anotherString`.
        - **Ноль (0)**: Если строки равны.
        - **Положительное значение**: Если текущая строка лексикографически больше строки `anotherString`.
    
    2. **Сравнение символов**:
        - Метод сравнивает строки символ за символом на основе их числовых значений (кодов в Unicode).
        - Сравнение происходит до тех пор, пока не найдётся первый несовпадающий символ.
        - Если одна строка является началом другой (например, "apple" и "applepie"), то более короткая строка считается меньшей.
    ##### Использование `compareTo` у строк:
    - **Сортировка строк**: Метод часто используется для сортировки строк в коллекциях:
    ```java
    import java.util.ArrayList;
    import java.util.Collections;
    
    public class StringSort {
        public static void main(String[] args) {
            ArrayList<String> list = new ArrayList＜＞();
            list.add("banana");
            list.add("apple");
            list.add("cherry");
    
            Collections.sort(list);
            System.out.println(list); // [apple, banana, cherry]
        }
    }
    ```
    
    - **Устранение чувствительности к регистру**: Если нужно сравнение без учёта регистра, используйте метод `compareToIgnoreCase` (`equalsIgnoreCase(` [^4]):
    [^4]:r

[^1]:> [!WARNING]
    **Возвращаемое значения:**
    > - **< 0**: текущий объект меньше переданного.
    > - **0**: объекты равны.
    > - **> 0**: текущий объект больше переданного.
    

[^5]:```java
    public class Person implements Comparable {
        String name;
    
        public Person(String name) {
            this.name = name;
        }
    
        @Override
        public String toString() {
            return '{' + name + '}';
        }
    
        @Override
        public int compareTo(Object o) { // Сравнение двух объектов Person
            Person other = (Person) o; // Приведение Object к типу Person
            return this.name.compareTo(other.name); // Сравнение строковых полей name
        }
    }
    
    class Main {
        public static void main(String[] args) {
            Person[] names = {new Person("Alice"), new Person("Charlie"), new Person("Bob")};
            Arrays.sort(names); // Вызовет compareTo
            System.out.println(Arrays.toString(names));
        }
    }
    ```

[^6]:> [!WARNING]
	**Возвращаемое значения:**
	> - **< 0**: текущий объект меньше переданного.
	> - **0**: объекты равны.
	> - **> 0**: текущий объект больше переданного.
	
	```java
	@Override  
	public int compareTo(Student other) {  
		return this.age - other.age; // Сортировка по возрасту  
	}  
	```
	#### Логика сравнения:
	```java
	return this.age - other.age;
	```
	- **`this.age`**: Возраст текущего объекта (того, на котором вызывается метод).
	- **`other.age`**: Возраст другого объекта, переданного в метод.
	- **`this.age - other.age`**:
	    - Если результат положительный, это значит, что текущий объект "больше" (старше).
	    - Если результат отрицательный, текущий объект "меньше" (младше).
	    - Если результат равен 0, оба объекта равны по возрасту.
[^7]:### Класс `StudentNameComparator`
	Этот класс реализует интерфейс `Comparator<Student>`, который используется для сравнения объектов типа `Student`. Он позволяет сортировать студентов по их именам в алфавитном порядке.
	```java
	class StudentNameComparator implements Comparator<Student> {
	    @Override
	    public int compare(Student s1, Student s2) {
	        return s1.getName().compareTo(s2.getName()); // реализация метода `compare()`
	    }
	}
	```
	### Разбор по частям:
	1. **`class StudentNameComparator implements Comparator<Student>`:**
	    - Класс `StudentNameComparator` реализует интерфейс `Comparator<Student>`, который предназначен для сравнения объектов типа `Student`. Это означает, что данный класс должен предоставить реализацию метода `compare()`, который будет использоваться для сравнения двух студентов.
	
	2. **`@Override`:**
	    - Аннотация `@Override` указывает, что метод `compare()` переопределяет метод интерфейса `Comparator`. Это гарантирует, что метод правильно реализован и соответствует его сигнатуре в интерфейсе.
	
	1. **`public int compare(Student s1, Student s2)`:**
	    - Метод `compare()` принимает два объекта типа `Student` (`s1` и `s2`).
	    - Он возвращает целое число:
	        - **Отрицательное значение**, если `s1` идет перед `s2` (по алфавиту).
	        - **Положительное значение**, если `s1` идет после `s2`.
	        - **0**, если они равны (имена одинаковые).
	
	1. **`return s1.getName().compareTo(s2.getName());`:**
	    - Этот код сравнивает имена двух студентов:
	        - `s1.getName()` и `s2.getName()` — это методы, которые возвращают имена студентов `s1` и `s2`.
	        - `compareTo()` — это метод строки, который выполняет алфавитное сравнение двух строк.
	            - Возвращает отрицательное число, если имя `s1` идет раньше в алфавите.
	            - Положительное число, если имя `s1` идет позже.
	            - 0, если имена одинаковые.

[^8]:```java
	String str1 = "Java";
	String str2 = "java";
	
	🔴int result1 = str1.compareToIgnoreCase(str2); // 0   (это значит строки равны)
	int result2 = str1.compareTo(str2);           // -32 (это значит вторая строка больше первой)
	
	Integer a = 15; // 
	Integer b = 10;
	int res = a.compareTo(b);  // 1 (данный метод есть и у Integer)
	int res = b.compareTo(a);  // -1
	```

[^9]:![[Снимок экрана 2024-12-21 в 19.57.26 1.png]]
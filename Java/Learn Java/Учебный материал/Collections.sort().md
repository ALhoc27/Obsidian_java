Метод `sort()` из класса `Collections` в Java используется для сортировки списка объектов. Он упрощает работу с сортировкой, предоставляя два основных варианта использования: сортировку по **естественному порядку элементов** [[java.lang.Comparable]] и сортировку с **использованием пользовательского(внешнего) компаратора**. [[java.util.Comparator]]

### Сигнатуры метода `sort()`
1. **Сортировка по естественному порядку элементов** [[java.lang.Comparable]]:
```java
public static <T extends Comparable<? super T>> void sort(List<T> list)
```
Этот метод сортирует список `list` в соответствии с естественным порядком элементов, который определяется интерфейсом `Comparable`.
2. **Сортировка с использованием компаратора** [[java.util.Comparator]]:
```java
public static <T> void sort(List<T> list, Comparator<? super T> c)
```
Этот метод сортирует список `list` с использованием компаратора `c`, который задает пользовательские правила сортировки.

<table class="language-java_td" style="width: 99%; border-collapse: collapse; margin-bottom: 5px;">
	<tr>
		<strong style="font-size: 1.1em; color: #333;">Пример:</strong>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333;"><span style="border: 1px solid black; padding: 2px;">#1</span>
&nbsp; Сортировка по естественному (ДЕФОЛТНОМУ) порядку элементов (Comparable):</strong>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333;"><span style="border: 1px solid black; padding: 2px;">#2</span>
&nbsp; Сортировка с использованием компаратора (Comparator):</strong>
        </td>
    </tr>
    <tr> 
        <td style="padding: 5px 10px; border: 1px solid #ddd;"> <strong>Естественный порядок</strong> для чисел — это порядок возрастания
            <pre class="language-java_td" style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
import java.util.*;
  
public class Main {
    public static void main(String[] args) {
        // Пример с числами
        List＜Integer＞ numbers = Arrays.asList(8, 3, 5, 2, 9);
         
        // Сортировка по естественному порядку
        Collections.sort(numbers);
         
        System.out.println(numbers); // [2, 3, 5, 8, 9]
    }
}
				</code>
            </pre>
            <strong>Естественный порядок</strong> для строк — это алфавитный порядок.
			<pre class="language-java_td" style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
import java.util.*;
 
public class Main {
    public static void main(String[] args) {
        List＜String> words = Arrays.asList("banana", "apple", "grape", "cherry");
         
        // Сортировка по алфавиту
        Collections.sort(words);
        
        System.out.println(words); // [apple, banana, cherry, grape]
    }
}
				</code>
            </pre>Метод использует реализацию <code>compareTo()</code> из класса <code>String</code>, где строки сравниваются лексикографически.
            
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
        Сортировка с использованием <strong>внешнего класса</strong>:
            <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
import java.util.*;
  
public class Main {
    public static void main(String[] args) {
        List＜Integer＞ numbers = Arrays.asList(8, 3, 5, 2, 9);
 
        // Сортировка в обратном порядке с использованием внешнего класса
        Collections.sort(numbers, new ReverseOrderComparator());
 
        System.out.println(numbers); // [9, 8, 5, 3, 2]
    }
}
  
// Внешний класс, реализующий Comparator
class ReverseOrderComparator implements Comparator＜Integer＞ {
    @Override
❗️    public int compare(Integer a, Integer b) {
        return b - a; // Обратный порядок
    }
 }
				</code>
            </pre>
        Сортировка с использованием <strong>анонимного класса</strong>:
            <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
import java.util.*;
 
public class Main {
    public static void main(String[] args) {
        List＜nteger＞ numbers = Arrays.asList(8, 3, 5, 2, 9);
 
        // Сортировка в обратном порядке с использованием анонимного класса
        Collections.sort(numbers, new Comparator＜Integer＞() {
            @Override
❗️            public int compare(Integer a, Integer b) {
                return b - a; // Обратный порядок
            }
        });
 
        System.out.println(numbers); // [9, 8, 5, 3, 2]
    }
}
				</code>
            </pre>
        <strong>Компаратор</strong> задается с помощью лямбда-выражения <code>(a, b) -> b - a</code>:
            <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
import java.util.*;
 
public class Main {
    public static void main(String[] args) {
        List＜Integer＞ numbers = Arrays.asList(8, 3, 5, 2, 9);
         
        // Сортировка в обратном порядке
❗️        Collections.sort(numbers, (a, b) -> b - a);
         
        System.out.println(numbers); // [9, 8, 5, 3, 2]
    }
}
				</code>
            </pre>
        </td>
    </tr>
</table>

<table class="language-java_td" style="width: 99%; border-collapse: collapse; margin-bottom: 5px;">
	<tr>
		<strong style="font-size: 1.1em; color: #333;">Пример с пользовательским классом:</strong>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333;"><span style="border: 1px solid black; padding: 2px;">#1</span>
&nbsp; Пример с пользовательским классом (java.lang.Comparable):</strong>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333;"><span style="border: 1px solid black; padding: 2px;">#2</span>
&nbsp; Пример с пользовательским классом (java.util.Comparator):</strong>
        </td>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre class="language-java_td" style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
import java.util.*;
 
class Person implements Comparable＜Person＞ {
    String name;
    int age;
 
    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
 
    @Override
    public int compareTo(Person other) {
        // Сортировка по возрасту
        return Integer.compare(this.age, other.age);
    }
 
    @Override
    public String toString() {
        return name + " (" + age + ")";
    }
}
 
public class Main {
    public static void main(String[] args) {
        List＜Person＞ people = Arrays.asList(
            new Person("Alice", 30),
            new Person("Bob", 25),
            new Person("Charlie", 35)
        );
 
        // Сортировка по возрасту (естественный порядок)
        Collections.sort(people);
 
        System.out.println(people); // [Bob (25), Alice (30), Charlie (35)]
    }
}
				</code>
            </pre>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
import java.util.*;
 
class Person {
    String name;
    int age;
 
    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
 
    @Override
    public String toString() {
        return name + " (" + age + ")";
    }
}
 
// Компаратор для сортировки по имени
class NameComparator implements Comparator＜Person＞ {
    @Override
    public int compare(Person p1, Person p2) {
        return p1.name.compareTo(p2.name);
    }
}
 
public class Main {
    public static void main(String[] args) {
        List＜Person＞ people = Arrays.asList(
            new Person("Alice", 30),
            new Person("Bob", 25),
            new Person("Charlie", 35)
        );
 
        // Сортировка по имени
        Collections.sort(people, new NameComparator());
 
        System.out.println(people); // [Alice (30), Bob (25), Charlie (35)]
    }
}
				</code>
            </pre>
        </td>
    </tr>
</table>

### Особенности метода
1. **Алгоритм сортировки**:
    - Используется модифицированный алгоритм **Timsort**, который является стабильным и имеет сложность ![[Снимок экрана 2024-12-20 в 03.25.05.png|80]] .

1. **Стабильность сортировки**:
    - Метод `Collections.sort()` является стабильным. Это означает, что порядок равных элементов сохраняется.

1. **Работа с `null`**:
    - Если список содержит `null`, то:
        - При естественном порядке будет выброшено исключение `NullPointerException`.
        - При использовании компаратора необходимо явно учитывать `null`, иначе также будет выброшено исключение.
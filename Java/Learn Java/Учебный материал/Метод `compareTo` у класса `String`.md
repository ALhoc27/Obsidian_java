```java
public int compareTo(String anotherString)
```
##### Как работает `compareTo` у `String`:
1. **Возвращаемое значение**:
    - **Отрицательное значение**: Если текущая строка лексикографически [^1] меньше строки `anotherString`.
    - **Ноль (0)**: Если строки равны.
    - **Положительное значение**: Если текущая строка лексикографически больше строки `anotherString`.

2. **Сравнение символов**:
    - Метод сравнивает строки символ за символом на основе их числовых значений (кодов в Unicode).
    - Сравнение происходит до тех пор, пока не найдётся первый несовпадающий символ.
    - Если одна строка является началом другой (например, "apple" и "applepie"), то более короткая строка считается меньшей.

##### Использование `compareTo` у строк:
- **Сортировка строк**: Метод часто используется для сортировки строк в коллекциях:

```java
import java.util.ArrayList;
import java.util.Collections;

public class StringSort {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("banana");
        list.add("apple");
        list.add("cherry");

        Collections.sort(list);
        System.out.println(list); // [apple, banana, cherry]
    }
}
```

- **Устранение чувствительности к регистру**: Если нужно сравнение без учёта регистра, используйте метод `equalsIgnoreCase()` :

### Так же есть метод для сравнения строк без учета регистра 'compareToIgnoreCase()'

```java
public int compareToIgnoreCase()
```
***Пример***
```java
String str1 = "Java";
String str2 = "java";

int result1 = str1.compareToIgnoreCase(str2); // 0   (это значит строки равны)
int result2 = str1.compareTo(str2);           // -32 (это значит вторая строка больше первой)

Integer a = 15; // 
Integer b = 10;
int res = a.compareTo(b);  // 1 (данный метод есть и у Integer)
int res = b.compareTo(a);  // -1
```

> [!TIP] Title
Статический метод  `compareTo()` есть так же и у других методов... [^2]


[^1]:![[Снимок экрана 2024-12-21 в 19.41.55.png|500]]
	
	Cравнивает символы в строках, начиная с самого первого, и продолжает сравнивать, пока не встретит различие или не достигнет конца одной из строк.


[^2]:![[Снимок экрана 2024-12-21 в 19.57.26.png]]


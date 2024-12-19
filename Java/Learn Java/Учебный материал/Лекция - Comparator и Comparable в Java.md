#### Содержание:
1. **Введение**
2. **`Comparable`**
    - Определение
    - Реализация
    - Примеры
3. **`Comparator`**
    - Определение
    - Реализация
    - Примеры
4. **Сравнение `Comparable` и `Comparator`**
5. **Практическое применение**
#### 1. Введение
В Java для сортировки объектов используется интерфейсы **Comparable** и **Comparator**. Они обеспечивают способ упорядочивания пользовательских объектов на основе определённых критериев.
- **Comparable**: Встроенное естественное упорядочивание.
- **Comparator**: Пользовательское (внешнее) упорядочивание.
---
#### 2. Comparable
###### Определение
Интерфейс **Comparable** (java.lang.Comparable) используется для определения **естественного порядка** объектов.
##### Основные моменты:
- Содержит единственный метод:
```java
  int compareTo(T o);
```
- Возвращаемые значения:
    - **Отрицательное значение**: текущий объект меньше переданного.
    - **Ноль**: объекты равны.
    - **Положительное значение**: текущий объект больше переданного.

***Реализация***
```java
public class Person implements Comparable<Person> {
    private String name;

    public Person(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    @Override
    public int compareTo(Person o) {
        return this.name.compareTo(o.name);
    }

    @Override
    public String toString() {
        return name;
    }
}
```

***Пример использования***
```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        Person[] people = {
            new Person("Charlie"),
            new Person("Alice"),
            new Person("Bob")
        };

        Arrays.sort(people); // Использует compareTo

        System.out.println(Arrays.toString(people));
    }
}
```
**Вывод:** `[Alice, Bob, Charlie]`

#### 3. Comparator
##### Определение
Интерфейс **Comparator** (java.util.Comparator) используется для создания **внешнего порядка** объектов.
##### Основные моменты:
- Содержит метод:
```java
int compare(T o1, T o2);
```
- Дополнительно можно использовать **default-методы**, такие как `reversed()` и `thenComparing()`.

***Реализация***
```java
import java.util.Comparator;

public class PersonComparator implements Comparator<Person> {
    @Override
    public int compare(Person p1, Person p2) {
        return p1.getName().compareTo(p2.getName());
    }
}
```

***Пример использования***
```java
import java.util.Arrays;
import java.util.Comparator;

public class Main {
    public static void main(String[] args) {
        Person[] people = {
            new Person("Charlie"),
            new Person("Alice"),
            new Person("Bob")
        };

        Arrays.sort(people, new PersonComparator()); // Внешний порядок

        System.out.println(Arrays.toString(people));
    }
}
```
**Вывод:** `[Alice, Bob, Charlie]`

##### Лямбда-выражение
```java
Arrays.sort(people, (p1, p2) -> p1.getName().compareTo(p2.getName()));
```

#### 4. Сравнение Comparable и Comparator
![[Снимок экрана 2024-12-19 в 21.51.52.png|650]]

#### 5. Практическое применение
- **Comparable**:
    - Удобно для объектов с единственным критерием сортировки.
    - Например, сортировка по имени, возрасту.
- **Comparator**:
    - Используется для сложных или множественных критериев.
    - Например, сортировка по имени, затем по возрасту:
```java
Comparator<Person> byNameThenAge = Comparator
    .comparing(Person::getName)
    .thenComparing(Person::getAge);
Arrays.sort(people, byNameThenAge);
```
#### Итоги
- **Comparable** используется для естественного порядка.
- **Comparator** даёт гибкость для сложных требований.
- Выбор зависит от задач:
    - Если нужен **один порядок** — используйте `Comparable`.
    - Для различных критериев — применяйте `Comparator`.
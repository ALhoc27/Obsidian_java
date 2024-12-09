### 1. **Установка окружения**

1. **JDK (Java Development Kit)**: Пакет для разработки на Java. Он включает в себя компилятор `javac` и JVM (Java Virtual Machine).
    - Скачать: [https://www.oracle.com/java/technologies/javase-downloads.html](https://www.oracle.com/java/technologies/javase-downloads.html)
        
2. **IDE или текстовый редактор**: Можно использовать IntelliJ IDEA, Eclipse или Sublime Text (если вы предпочитаете лёгкий редактор).
    
3. **[[Maven]]** (опционально) или **[[Gradle]]**: Система управления зависимостями и сборкой для проектов на Java.
    

Проверка установки:
```bash
java -version
javac -version
```

---

### 2. **Первая программа на Java**
Создадим простой класс с выводом «`Hello, World!`» на экран.

**Код:**

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```


**Объяснение:**
- `public:` Доступен всем.
- `class`: Объявляет класс.
- `main`: Это точка входа в программу. JVM ищет метод `main` для начала выполнения.
- `String[] args`: Аргументы командной строки.
- `System.out.println()`: Выводит текст в консоль.


**Компиляция и запуск:**

javac HelloWorld.java
java HelloWorld

---

### 3. **Переменные и типы данных**

В Java необходимо объявлять тип переменной перед ее использованием.

**Пример:**

int age = 25;              // Целое число
double price = 19.99;       // Число с плавающей точкой
char letter = 'A';          // Символ
boolean isJavaFun = true;   // Логический тип
String name = "Alice";      // Строка

#### Примитивные типы данных:

- `byte`, `short`, `int`, `long` – целые числа.
    
- `float`, `double` – числа с плавающей точкой.
    
- `char` – символы.
    
- `boolean` – логический тип (true/false).
    

---

### 4. **Управляющие конструкции**

#### Условные операторы (`if`/`else`):

int number = 10;
if (number > 0) {
    System.out.println("Положительное число");
} else {
    System.out.println("Отрицательное число");
}

#### Циклы:

1. `for`:

for (int i = 0; i < 5; i++) {
    System.out.println(i);
}

2. `while`:

int i = 0;
while (i < 5) {
    System.out.println(i);
    i++;
}

---

### 5. **Методы**

Метод — это блок кода, который выполняет определённую задачу.

#### Пример метода:

public class Calculator {
    public static int add(int a, int b) {
        return a + b;
    }

    public static void main(String[] args) {
        int result = add(5, 3);
        System.out.println("Результат: " + result);
    }
}

#### Объяснение:

- `int add(int a, int b)`: Метод принимает два параметра и возвращает сумму.
    
- Вызов метода из `main`: `add(5, 3)`.
    

---

### 6. **Классы и объекты**

Java поддерживает объектно-ориентированное программирование (ООП). Основные концепции:

- **Класс** — это шаблон для создания объектов.
    
- **Объект** — экземпляр класса.
    

#### Пример:

public class Car {
    String model;
    int year;

    // Конструктор
    public Car(String model, int year) {
        this.model = model;
        this.year = year;
    }

    public void displayInfo() {
        System.out.println("Модель: " + model + ", Год: " + year);
    }

    public static void main(String[] args) {
        Car car1 = new Car("Toyota", 2020);
        car1.displayInfo();
    }
}

#### Объяснение:

- Конструктор используется для инициализации объекта.
    
- Метод `displayInfo()` выводит информацию о машине.
    

---

### 7. **Коллекции и массивы**

#### Массив:

int[] numbers = {1, 2, 3, 4, 5};
System.out.println(numbers[0]);  // Выводит 1

#### ArrayList:

import java.util.ArrayList;

public class Example {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("Java");
        list.add("Python");
        System.out.println(list);
    }
}

---

### 8. **Исключения**

Исключения (exceptions) обрабатывают ошибки во время выполнения.

#### Пример обработки:

try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Ошибка: Деление на ноль!");
} finally {
    System.out.println("Блок finally выполняется всегда.");
}

---

### 9. **Работа с Maven**

Если вы используете Maven, создайте проект и добавьте зависимости в файл `pom.xml`.

<dependencies>
    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-lang3</artifactId>
        <version>3.12.0</version>
    </dependency>
</dependencies>

Для сборки проекта:

mvn compile
mvn exec:java -Dexec.mainClass="com.example.Main"

---

## 10. **Заключение и дальнейшие шаги**

После освоения основ Java вы можете углубиться в следующие темы:

1. **ООП**: Наследование, полиморфизм, интерфейсы.
    
2. **Потоки (Threads)** и многопоточность.
    
3. **Работа с базами данных** (JDBC, Hibernate).
    
4. **Веб-приложения** (Spring, Java EE).
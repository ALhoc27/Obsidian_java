https://struchkov.dev/blog/ru/memory-in-java/
### **Структура памяти JVM**

1. ##### **[[Heap (Куча)]]** [^8]
	- **Young Generation (Молодое поколение):**
	    - **Eden Space:** Область для новых объектов.
	    - **Survivor Spaces (S0 и S1):** Объекты, которые пережили первую фазу сборки мусора.[^9] 
	- **Old Generation (Старое поколение):**
	    - Для долгоживущих объектов, перемещённых из молодого поколения.
	- **Metaspace (с Java 8):**
	    - Хранит метаданные классов, включая: 
		    - Информацию о полях, методах, конструкторах.
		    - Таблицы виртуальных методов.
		    - Ссылки на статические поля (хранятся отдельно от самих данных).
	    - Пул строк (**[[String Pool]]**) — хранит литералы строк для оптимизации памяти.
1. ##### **[[Stack (Стек)]]** [^7]
	- Уникален для каждого потока.
	- Автоматически освобождается при завершении методов.
2. ##### **[[Method Area (Область методов)]]** ^[Хранит метаданные классов]
	- Информация о структуре классов (поля, методы, конструкторы).
	- Статические переменные.
	- Константы.
3. ##### **PC Register (Счётчик команд)**
	- Указывает текущую инструкцию, исполняемую JVM.
	- Каждый поток имеет свой собственный PC-регистр.
4. ##### **Native Method Stack**
	- Используется для вызовов методов, написанных на нативных языках (например, C или C++).
	- Хранит информацию о вызовах, аргументах и данных для нативного кода.




## **Heap (Куча)**
Куча используется для хранения объектов и данных, которые имеют динамическое время жизни.
### Что попадает в **Heap (Куча)**
1. **Экземпляры классов** [^1]
2. **Массивы**[^2]
3. **Анонимные и вложенные классы** [^3]
4. **Ссылочные типы**: Если поле класса или переменная является ссылкой на объект, то сам объект создаётся в куче [^4]
5. **Литералы строк (в String Pool)** [^5]
6. **Объекты `String`, созданные явно через `new`** [^6]
#### *Что не хранится в куче*
- **Локальные переменные** методов — они размещаются в **стеке**.
- **Параметры метода** — хранятся в **стеке**.
- **Примитивные типы данных**, если они являются локальными переменными, также размещаются в **стеке**.

### Из чего состоит куча
Куча (**Heap**) в Java состоит из нескольких ключевых областей памяти, которые управляются JVM для эффективного размещения и удаления объектов. Основная цель разделения — оптимизация работы с объектами разной продолжительности жизни.

>**Структура:**
> - **Young Generation (Молодое поколение):**
>     - **Eden Space:** Новые объекты.
>     - **Survivor Spaces (S0 и S1):** Объекты, пережившие первую фазу сборки мусора.
> - **Old Generation (Старое поколение):**
>     - Долгоживущие объекты, перемещённые из молодого поколения.
> - **Metaspace (с Java 8):**
>     - Метаданные классов (заменило Permanent Generation).

Подробнее:

##### 1. **Young Generation (Молодое поколение)**
Эта область предназначена для новых объектов, которые только что созданы.

- **Подразделы:**
    - **Eden Space**:
        - Все новые объекты сначала попадают сюда.
        - Область часто очищается сборщиком мусора (**Minor GC**).
    - **Survivor Space (S0 и S1)**:
        - Объекты, которые "выжили" одну или несколько фаз сборки мусора из Eden, перемещаются сюда.
        - Используется для фильтрации объектов, которые могут быть долгоживущими.
        - Есть две области Survivor: `S0` и `S1`, между которыми объекты перемещаются.
##### Ключевые особенности:
- Частая сборка мусора (быстрая и эффективная).
- Большинство объектов здесь "умирает" очень быстро.
- Объекты, которые пережили несколько циклов сборки, перемещаются в **Old Generation**.

##### 2. **Old Generation (Старое поколение)**
Эта область предназначена для долгоживущих объектов, которые "пережили" несколько сборок мусора в Young Generation.
##### Ключевые особенности:
- Хранит объекты, которые активно используются в течение долгого времени.
- Очистка проводится менее часто, чем в Young Generation, и требует больше времени (**Major GC** или **Full GC**).
- Эффективно для объектов, которые редко изменяются (например, кэш или крупные коллекции).

##### 3. **Metaspace (Метапространство)**
С Java 8 область **Permanent Generation** была заменена на **Metaspace**.
###### Ключевые особенности:
- Хранит метаданные классов:
    - Информацию о полях, методах, конструкторах.
    - Статические поля и их ссылки.
    - Пул символов (String Pool).
- Метасвязанные данные теперь размещаются вне основного пространства кучи (в нативной памяти).
- Размер Metaspace адаптируется динамически, ограничен памятью устройства.

##### 4. **String Pool (Пул строк)**
Специальная часть кучи для хранения **литералов строк**.

- **Особенности:**
    - Литералы строк переиспользуются для оптимизации памяти.
    - Пул строк был перенесён в кучу (Heap) с Java 7.

##### 5. **Code Cache (Кэш кода JIT-компилятора)**
Эта область используется для хранения скомпилированного машинного кода, созданного JIT-компилятором.

- Улучшает производительность, позволяя JVM повторно использовать уже скомпилированный код.

### Особенности:
- **Общие данные:** Объекты, создаваемые с помощью `new`, и их поля.
- **Сборщик мусора (Garbage Collector):** Автоматически удаляет объекты, на которые больше нет ссылок.
- **Структура:**
    - **Young Generation (Молодое поколение):**
        - **Eden Space:** Новые объекты.
        - **Survivor Spaces (S0 и S1):** Объекты, пережившие первую фазу сборки мусора.
    - **Old Generation (Старое поколение):**
        - Долгоживущие объекты, перемещённые из молодого поколения.
    - **Metaspace (с Java 8):**
        - Метаданные классов (заменило Permanent Generation).

***Пример:***
```java
String s = new String("Hello"); // Объект создаётся в куче.
```

## 2. **Stack (Стек)**

Стек хранит данные методов, включая:
- Локальные переменные.
- Ссылки на объекты в куче.
- Результаты вычислений.

### Особенности:
- Каждая нить имеет свой стек.
- Быстрый доступ (LIFO — Last In, First Out).
- Память автоматически освобождается при выходе из метода.

***Пример:***
```java
void method() {
    int x = 10; // Переменная хранится в стеке.
    String s = "Hello"; // Ссылка хранится в стеке, а объект — в куче.
}
```

## 3. **Method Area (Область методов)**
Эта область памяти предназначена для хранения метаданных классов.
### Особенности:
- Содержит:
    - Структуры классов (поля, методы, конструкторы).
    - Статические поля.
    - Константы.
- Это общая область памяти для всех потоков.
- Реализована в **Metaspace** начиная с Java 8.

***Пример:***
```java
class MyClass {
    static int staticVar = 10; // Хранится в Method Area.
}
```

## 4. **Program Counter Register (Счётчик команд)**
Каждый поток имеет собственный **PC-регистр**, который указывает на текущую инструкцию, исполняемую JVM.
### Особенности:
- Используется для отслеживания последовательности выполнения команд.
- Если поток выполняет нативный код, значение PC-регистра — неопределённое.

## 5. **Native Method Stack**
Хранит данные, связанные с вызовом нативных методов (например, методов, написанных на C или C++).
### Особенности:
- Используется для интеграции с нативными библиотеками.
- Включает информацию о вызовах методов и их аргументах.


![[Снимок экрана 2024-12-15 в 13.02.07.png|650]]


[^1]:```java
	class MyClass {
	    int x; // Поле экземпляра
	}
	MyClass obj = new MyClass(); // Объект `obj` находится в куче
	```
[^2]:```java
	int[] array = new int[10]; // Массив хранится в куче
	```
[^3]:```java
	Runnable r = new Runnable() {
	    @Override
	    public void run() {
	        System.out.println("Anonymous class");
	    }
	}; 
	// Экземпляр анонимного класса находится в куче
	```
[^4]:```java
	class Node {
	    Node next; // Ссылка на другой объект в куче
	}
	Node head = new Node(); // Объект head хранится в куче
	```
[^5]:```java
	String s = "Hello"; // Литерал "Hello" хранится в String Pool, который является частью кучи
	```
[^6]:```java
	String s = new String("Hello"); 
	// Новый объект строки создаётся в куче, несмотря на наличие "Hello" в String Pool
	```
[^7]:Хранит вызовы методов и локальные переменные.
	#### Cтек и куча в Java
	Основное отличие стека и кучи в Java от их общего представления связано с автоматическим управлением памятью.==В Java не нужно явно освобождать память в куче, так как этим занимается сборщик мусора.==Если на объект, на который ссылается локальная переменная, больше нет ссылок, он становится доступным для сборщика мусора.
	
	Пространство стека ограничено и обычно меньше пространства кучи. Если приложение попытается использовать больше стековой памяти, чем доступно, это приведёт к `ошибкеStackOverflowError`.
	
	Куча в Java — это область памяти, где создаются все объекты. Когда вы создаёте объект с помощью оператора`new`, он размещается в куче.

[^8]:Используется для хранения объектов и данных, имеющих динамическое время жизни.
	#### Cтек и куча в Java
	Основное отличие стека и кучи в Java от их общего представления связано с автоматическим управлением памятью.==В Java не нужно явно освобождать память в куче, так как этим занимается сборщик мусора.==Если на объект, на который ссылается локальная переменная, больше нет ссылок, он становится доступным для сборщика мусора.
	
	Пространство стека ограничено и обычно меньше пространства кучи. Если приложение попытается использовать больше стековой памяти, чем доступно, это приведёт к `ошибкеStackOverflowError`.
	
	Куча в Java — это область памяти, где создаются все объекты. Когда вы создаёте объект с помощью оператора`new`, он размещается в куче.

[^9]:[[Garbage Collection в Java (Сборка мусора)]]
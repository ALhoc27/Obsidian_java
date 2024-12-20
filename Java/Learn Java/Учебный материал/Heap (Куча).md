Куча (**Heap**) — это область памяти JVM, предназначенная для хранения объектов и данных с динамическим временем жизни. Она организована таким образом, чтобы обеспечить эффективное управление памятью, сборку мусора и производительность приложения.

|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <span style="font-size: 1.3em; font-weight: bold; margin: 0; line-height: 1.2; display: inline-block; margin-bottom: 10px;"> &nbsp;&nbsp;Куча</span><br>Куча — это область памяти, динамический распределяемая во время выполнения программы. В отличие от стека, ==**данные в куче могут существовать дольше**, чем отдельные вызовы функций, а объёмы памяти, выделяемой в куче, обычно гораздо больше, чем в стеке.==<br><br>Динамическое управление памятью подразумевает процесс выделения и освобождения памяти в куче во время работы программы. Когда программе требуется память для хранения данных, она может запросить у операционной системы блок памяти в куче, достаточно большой для этих данных.<br><br>==Однако важно помнить, что, в отличие от стека, память в куче не освобождается автоматически.== Когда данные больше не нужны, программа должна явно указать операционной системе, что эту память можно освободить для использования другими процессами. Этот процесс называется **“освобождение памяти”.**<br><br>==Если программа продолжает использовать память, не освобождая её, это может привести к “утечке памяти”==, когда значительные объёмы памяти заняты данными, которые уже не нужны. Это может вызвать снижение производительности и, в конечном итоге, привести к ошибкам, когда вся доступная память будет исчерпана.<br><br><br><br><br> ![[Pasted image 20241215220307.png\|650]]<br><br>**Объекты могут содержать методы, а методы — локальные переменные. Эти локальные переменные хранятся в стеке потока, даже если сам объект, которому принадлежат методы, находится в куче.**<br><br><br><span style="font-size: 1.4em; font-weight: bold; margin: 0; line-height: 1.2; display: inline-block; margin-bottom: 10px;"> &nbsp;&nbsp;Особенности</span><br>- **Динамическое распределение памяти**: Куча позволяет программе запрашивать необходимый объём памяти динамически и использовать его до тех пор, пока программа не освободит его.<br>- **Долговечность данных**: Память в куче не освобождается автоматически, поэтому данные могут существовать до тех пор, пока не будут явно удалены, что позволяет им пережить вызовы функций.<br>- **Управление памятью**: Работа с кучей требует тщательного управления памятью. Утечки памяти могут стать проблемой, если память не освобождается своевременно.<br>- **Медленный доступ**: Доступ к данным в куче может быть медленнее по сравнению со стеком, из-за более сложного управления и отсутствия локализации данных.<br><br> |

### **Общая структура кучи**
Куча разделена на **поколения объектов**, каждое из которых имеет свои характеристики:

1. **Молодое поколение (Young Generation)**.
2. **Старое поколение (Old Generation)**.
3. **Metaspace (с Java 8)**.
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

### Из чего состоит куча:
Куча (**Heap**) в Java состоит из нескольких ключевых областей памяти, которые управляются JVM для эффективного размещения и удаления объектов. Основная цель разделения — оптимизация работы с объектами разной продолжительности жизни. ([[Области памяти в java]]) 
![[Снимок экрана 2024-12-16 в 00.12.27.png|600]]

#### ==1. **Молодое поколение (Young Generation)**==
Эта область используется для новых объектов, которые только что созданы.
#### Подразделы молодого поколения:
1. **Eden Space (Область Эдема):**
    - Все новые объекты сначала размещаются здесь.
    - Большая часть объектов "умирает" в этой области, так как их время жизни короткое.
    - Если объект переживает сборку мусора, он перемещается в область Survivor.
    - **Пример:** Объекты временных коллекций, локальные строки.

2. **Survivor Spaces (S0 и S1):**
    - Хранят объекты, которые пережили одну или несколько сборок мусора в Eden Space.
    - Используется для фильтрации долгоживущих объектов.
    - Есть две области Survivor:
        - **S0:** первая область.
        - **S1:** вторая область.
    - После нескольких сборок мусора (определяется порогом) объект перемещается в **старое поколение**.
#### Характеристики:
- Частая сборка мусора в Young Generation (**Minor GC**).
- Память быстро освобождается.
- Объекты, которые не выживают, удаляются.
#### ==2. **Старое поколение (Old Generation)**==
Старое поколение предназначено для долгоживущих объектов.
#### Особенности:
- Объекты, пережившие несколько сборок мусора в Young Generation, перемещаются сюда.
- Большая часть памяти выделяется для объектов, которые остаются активными долгое время.
- Сборка мусора в этой области называется **Major GC** (или **Full GC**).
    - **Major GC** происходит реже, но требует больше времени.
#### Пример объектов:
- Кэш объектов.
- Большие коллекции данных.
- Глобальные строки, хранимые на протяжении всей работы приложения.

#### **==4. Metaspace (Метапространство)==**
С Java 8 область **Permanent Generation** была заменена на **Metaspace**.
#### Что хранится в Metaspace:
- Метаданные классов, включая:
    - Информацию о методах, конструкторах, полях классов.
    - Таблицы виртуальных методов.
    - Ссылки на статические поля (хранятся отдельно от самих данных).
- Пул строк (**[[String Pool]]**) — хранит литералы строк для оптимизации памяти.

#### Особенности Metaspace:
- Хранится в нативной памяти, а не в куче.
- Размер может изменяться динамически.

### **Как работает ==сборка мусора (Garbage Collection) в куче==**

1. **Minor GC (Молодая сборка мусора):**
    - Очищает Eden Space и объекты из Survivor Spaces.
    - Быстрая и частая операция.
    - Перемещает выжившие объекты в Old Generation.

1. **Major GC (Старшая сборка мусора):**
    - Очищает старое поколение.
    - Редкая, более затратная операция.

1. **Full GC:**
    - Полная очистка всей кучи, включая молодое и старое поколения.
    - Происходит только в крайних случаях (например, при нехватке памяти).

[[Garbage Collection в Java (Сборка мусора)]]




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

`java.util.stream.Collectors` — это утилитный класс в Java Stream API, который предоставляет набор методов для **сборки (collecting)** данных из потоков (Stream) в различные структуры данных, такие как списки, множества, карты, а также для выполнения операций агрегирования, таких как суммирование или объединение строк. `Collectors` часто используется в методе `.collect(...)`, который является терминальной операцией потока и позволяет собрать элементы из потока в нужную структуру.

#### Основные методы Collectors:[^4]
1. **`toList()`** - Собирает элементы потока в `List`
```java
List<String> list = stream.collect(Collectors.toList());
```
2. **`toSet()`** - Собирает элементы в `Set`, что полезно, если нужны уникальные значения:
```java
Set<String> set = stream.collect(Collectors.toSet());
```
3. **`toMap()`** - Преобразует поток в `Map`, где каждый элемент потока становится записью (ключ-значение):
```java
Map<Integer, String> map = stream.collect(Collectors.toMap(String::length, Function.identity()));
```
- [^3] Здесь `String::length`[^1] используется как ключ, а `Function.identity()`[^2] возвращает исходное значение элемента для значения `Map`.

4. **`joining()`** - Объединяет элементы потока в строку. Может принимать разделитель и опционально префикс и суффикс:
```java
String result = stream.collect(Collectors.joining(", ", "[", "]"));
```
5. **`groupingBy()`** - Группирует элементы потока по ключу, создавая `Map`, где каждый ключ связан со списком элементов:
```java
Map<Integer, List<String>> groupedByLength = stream.collect(Collectors.groupingBy(String::length));
```
- Здесь строки группируются по длине, и каждый ключ (длина строки) связывается с `List` строк данной длины.
  
6. **`partitioningBy()`** - Разделяет элементы на две группы по условию. Возвращает `Map` с булевыми ключами (`true` и `false`):
```java
Map<Boolean, List<String>> partitioned = stream.collect(Collectors.partitioningBy(s -> s.length() > 3));
```
7. **`summarizingInt(), summarizingDouble(), summarizingLong()`** - Создает статистику (например, количество, сумму, среднее, минимум, максимум) для числовых данных:
```java
IntSummaryStatistics stats = stream.collect(Collectors.summarizingInt(String::length));
```
8. **`counting()`** - Возвращает количество элементов в потоке:
```java
long count = stream.collect(Collectors.counting());
```
9. **`reducing()`** - Выполняет операции редукции, где каждый элемент потока комбинируется для получения одного значения:
```java
Optional<String> concatenated = stream.collect(Collectors.reducing((s1, s2) -> s1 + s2));
```

#### Примеры использования Collectors
Допустим, у вас есть список строк, и вы хотите отфильтровать, отсортировать и собрать их в список, используя `Collectors`:
```java
List<String> strings = List.of("apple", "banana", "cherry", "date");
List<String> result = strings.stream()
                             .filter(s -> s.length() > 4)
                             .sorted()
                             .collect(Collectors.toList());
```
#### Зачем использовать Collectors?

`Collectors` предоставляет гибкий и мощный способ обработки данных, собирая их в различные структуры данных. Он упрощает работу с потоками и делает код более читаемым и кратким. Особенно полезен для обработки больших наборов данных, выполняя операции группировки, суммирования и агрегации, которые было бы сложно реализовать обычными циклами.


[^1]:`String::length` — пример ссылки на метод (method reference) в Java, введенная в Java 8. Она указывает на метод `length` класса `String` и позволяет вызывать его в функциональном стиле, например, при работе с лямбда-выражениями или потоками.
	
	- `String` — это класс, в котором находится метод `length`.
	- `::length` — это ссылка на метод `length`.
	##### Синтаксис:
	```java
	public int length()
	```
	Метод `length()` в классе `String` возвращает количество символов в строке, на которой он вызывается. Этот метод полезен для определения **длины строки**, включая пробелы и другие специальные символы.
	
	Вызывается метод у любой строки (обьекта типа `**String**`), возвращается число символов (число - `**int**`)
	
	**Примечание**: Длина строки равна числу символов Unicode (UTF-16 code units), которые составляют строку.
	<hr/>
	
	`String::length` аналог `s -> s.length()` (лямбда выражение)
	
	

[^2]:`Function.identity()` — это статический метод в Java, который возвращает **функцию, которая просто возвращает свой входной параметр** без изменений. Он определяется в интерфейсе `java.util.function.Function`.
	
	##### Зачем нужен `Function.identity()`?
	
	`Function.identity()` полезен, когда нужно передать функцию, которая ничего не делает с входным значением, а просто возвращает его. Это особенно полезно в ситуациях, когда требуется функция в качестве параметра, но в вашем случае преобразования не нужны.

[^3]:```java
	Stream<String> stream = Arrays.stream(array);
	
	Map<Integer, String> map = stream.collect(Collectors.toMap(String::length, Function.identity()));
	```
	- `stream` уже предполагает, что это **существующий поток** (например, `Stream<String> stream = Arrays.stream(array);`), который должен быть создан до выполнения этого кода.
	- Это значит, что `stream` уже является потоком данных, и его можно сразу обрабатывать.
	**Аналог**:
	```java
	Map<Integer, String> map = Arrays.stream(array) .collect(Collectors.toMap(String::length, Function.identity()));
	```
	- `Arrays.stream(array)` — это создание потока (Stream) из массива `array`. Массив `array` должен быть заранее определен (например, `String[] array = {"apple", "banana", "cherry"};`).
	- Сначала массив превращается в поток с помощью `Arrays.stream()`, а затем данные собираются в карту с помощью `Collectors.toMap`.

[^4]:В примерах ниже `stream` уже предполагает, что это **существующий поток** (например, `Stream<String> stream = Arrays.stream(array);`), который должен быть создан до выполнения этого кода.
	```java
	Stream<String> stream = Arrays.stream(array);
	List<String> list = stream.collect(Collectors.toList());
	```
	##### Аналог (более краткая форма)
	
	```java
	List<String> list = Arrays.stream(array).collect(Collectors.toList());
	```
	
	
В Java объект класса `Class` представляет метаданные о классе или интерфейсе в вашей программе. **Это часть механизма рефлексии**, которая позволяет динамически исследовать или изменять поведение программы во время выполнения.
╒╤╤╤ 🔎 [[Рефлексия]] 🔍 ╤╤╤╤╕

#### Что за тип Class в Java?
В Java почти все сущности являются объектами, за исключением примитивных типов. У каждого объекта есть класс. Сами классы тоже является объектами, и они принадлежат классу Class.

> [!TIP]
> **Class** - **это generic тип**. Методы Class предназначены для получения информации о классе (объекте типа Class). У класса Class нет публичных конструкторов. 

Например: можно узнать ***полное имя класса***, ***какие у него аннотации***, ***какие конструкторы и т.п.*** ==Эти методы нужны для reflection==. С помощью reflection вы можете создавать объекты, которые принадлежат этому классу, и при этом заранее класс объекта вы можете не знать.

Существуют библиотеки, которые позволяют создавать объекты типа Class "на лету", т.е. вы можете создать новый класс прямо во время работы программы и так же можете изменить существующий класс.

### **Что такое объект `Class`?**

Каждый загруженный JVM класс или интерфейс автоматически ассоциируется с объектом типа `Class`. Этот объект:
- Содержит информацию о классе, такой как его имя, модификаторы доступа, методы, поля и конструкторы.
- Используется для создания новых экземпляров класса, вызова методов, анализа структуры и прочих операций.

Пример:
```java
public class Example {
    public static void main(String[] args) {
        Class<?> clazz = String.class; // Получение объекта Class
        System.out.println("Имя класса: " + clazz.getName());
    }
}
```

Результат:
``` yaml
Имя класса: java.lang.String
```

### **Как получить объект класса `Class`**
1. **Использование `.class`:**
```java
Class<?> clazz = String.class;
```
<br>

2. **Через метод `getClass()` у объекта:**
```java
String str = "Hello"; 
Class<?> clazz = str.getClass();
```
<br>

3. **Через метод `Class.forName()`:**
```java
try {
    Class<?> clazz = Class.forName("java.util.ArrayList");
} catch (ClassNotFoundException e) {
    e.printStackTrace();
}
```

### **Методы класса `Class`**

Объект `Class` предоставляет множество методов для работы с метаданными:

#### **1. Получение информации о классе:**
- `getName()`: Возвращает полное имя класса.
- `getSimpleName()`: Возвращает простое имя класса.
- `getPackage()`: Возвращает пакет, к которому принадлежит класс.
- `getSuperclass()`: Возвращает родительский класс (для объектов, кроме `Object`).

**Пример:**
```java
Class<?> clazz = String.class;
System.out.println("Полное имя: " + clazz.getName());
System.out.println("Простое имя: " + clazz.getSimpleName());
System.out.println("Пакет: " + clazz.getPackage());
System.out.println("Родительский класс: " + clazz.getSuperclass());
```

#### **2. Работа с методами и конструкторами:**
- `getMethods()`: Возвращает массив всех публичных методов (включая унаследованные).
- `getDeclaredMethods()`: Возвращает только методы, объявленные в данном классе.
- `getConstructors()`: Возвращает массив конструкторов.
- `getDeclaredConstructors()`: Возвращает только объявленные конструкторы.

**Пример:**
```java
Class<?> clazz = String.class;
for (var method : clazz.getDeclaredMethods()) {
    System.out.println("Метод: " + method.getName());
}
```

#### **3. Работа с полями:**
- `getFields()`: Возвращает публичные поля.
- `getDeclaredFields()`: Возвращает все поля, объявленные в классе.

**Пример:**
```java
Class<?> clazz = Math.class;
for (var field : clazz.getDeclaredFields()) {
    System.out.println("Поле: " + field.getName());
}
```

#### **4. Создание экземпляров:**
- `newInstance()`: Создаёт новый экземпляр класса (устарело с Java 9, лучше использовать конструкторы).

**Пример:**
```java
try {
    Class<?> clazz = String.class;
    String str = (String) clazz.getDeclaredConstructor(String.class).newInstance("Hello");
    System.out.println("Созданный объект: " + str);
} catch (Exception e) {
    e.printStackTrace();
}
```
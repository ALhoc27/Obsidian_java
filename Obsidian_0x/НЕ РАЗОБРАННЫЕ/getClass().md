- *[[instanceof()]]*
- *[[java.lang.Class<T>]]*

Метод `getClass()` — это метод класса `Object`, который есть у всех объектов в Java. Его основная задача — возвращать метаинформацию о классе объекта, включая его точный тип. Это позволяет разработчикам узнать, к какому классу принадлежит объект во время выполнения программы.

#### Сигнатура метода `getClass()` [^1]
```java
public final native Class<?> getClass();
```
#### **Что возвращает `getClass()`?**

Метод возвращает объект типа [[java.lang.Class<T>]], который представляет:
- Имя класса.
- Список полей, методов и конструкторов класса.
- Информацию о родительском классе и интерфейсах.
**Пример:**
```java
class Animal {}
class Dog extends Animal {}

public class Main {
    public static void main(String[] args) {
        Animal animal = new Dog(); // Объект подкласса Dog
🔴      System.out.println(animal.getClass()); // class Dog
    }
}
```

> [!WARNING] Важно
> - Представляет **тип (класс)** объекта во время выполнения программы (runtime).
> - **`getClass()`** возвращает точный класс объекта(**фактический тип объекта**), с которым он вызывается. (**строгое соответствие классу**, ни каких наследников только точный класс объекта)
> 	&nbsp;&nbsp;&nbsp;&nbsp; 🔴	*`animal` относится к типу `Animal`, но его фактический класс (runtime class) — `Dog`.*<br/>
> 	&nbsp;
> - Метод `getClass()` является **`final`** в классе `Object`, поэтому его нельзя переопределить.
> - У каждого класса в Java есть только один объект `Class`. (Этот объект создаётся автоматически и хранится в памяти. Все вызовы `getClass()` для объектов одного класса возвращают один и тот же объект `Class`) [^2]
> - Метод `getClass()` в Java не может быть вызван на значении `null`. Если попытаться вызвать `getClass()` на `null`, произойдёт **исключение** **`NullPointerException`**.
> - **Не учитывает интерфейсы.** Если объект реализует интерфейс, `getClass()` не будет показывать это. 
> - Не подходит для случаев, когда нужно учитывать наследование (в таких ситуациях лучше использовать `instanceof`)

**Пример:**
```java
class Parent {
    private String name;

    public Parent(String name) {
        this.name = name;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
🔴      if (obj == null || getClass() != obj.getClass()) return false;
        Parent parent = (Parent) obj;
        return name.equals(parent.name);
    }
}

class Child extends Parent {
    public Child(String name) {
        super(name);
    }
}
```

> [!WARNING] #### `getClass()` в Java никогда не может быть вызван на значении `null` (**Необходимо проверять объект на `null` перед вызовом `getClass()`**)
>```java
>🔴 if (obj == null || getClass() != obj.getClass()) return false; // || означает что хотя бы одно из условий достаточно для выполнения блока `return false`
>```
>(**Логическое "или" (`||`)** означает, что хотя бы одно из условий достаточно для выполнения блока `return false`. Если `obj == null`, вернётся `false`. Если классы объектов разные (`getClass() != obj.getClass()`), вернётся `false`.)
>  
> - Метод `getClass()` вызывается на объекте. Если объект равен `null`, значит, он не существует в памяти, и его класс неизвестен.
> - Попытка обратиться к методу объекта, который равен `null`, приводит к попытке доступа к несуществующей ссылке, что вызывает **исключение** **`NullPointerException`**.<br/>
> &nbsp;
> - `instanceof` в отличии от  `getClass()` **==безопасен для использования с==** **`null`**. Если объект равен `null`, выражение с `instanceof` просто вернёт `false`, а не выбросит исключение. 
 


<table class="language-java_td" style="width: 99%; border-collapse: collapse; margin-bottom: 5px;">
	<tr>
		<strong style="font-size: 1.1em; color: #333;">Пример :</strong>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333; line-height: 1.7;"><span style="border: 1px solid black; padding: 2px;">#1</span>
&nbsp; Пример 1</strong><br/>
<b>Возвращаемое значение</b>: Метод возвращает объект типа <code>Class</code>. Класс <code>Class</code> представляет собой метаданные о конкретном классе, такие как имя класса, суперкласс, методы, поля и так далее.
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333; line-height: 1.7;"><span style="border: 1px solid black; padding: 2px;">#2</span>
&nbsp; Пример 2<br/></strong>
        </td>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre class="language-java_td" style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
Object obj = new String("Пример");
Class＜?＞ clazz = obj.getClass();
System.out.println(clazz.getName()); // Выведет "java.lang.String"
				</code>
            </pre>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
class Person {}
	   
public class Main { 
    public static void main(String[] args) { 
        Person person = new Person(); 
        System.out.println(person.getClass()); // Вывод: class Person 
    } 
} 
				</code>
            </pre>
        </td>
    </tr>
</table>

> [!NOTE] **Метод возвращает объект типа [[java.lang.Class<T>]]**
>Метод `getClass()` возвращает объект типа `Class<?>`, который предоставляет метаинформацию о классе объекта. Класс `Class` в Java содержит множество методов, позволяющих получить данные о классе, включая его поля, методы, интерфейсы, конструкторы и другие характеристики.
>
>**Рефлексия**: Методы класса `Class` позволяют получить доступ ко всем аспектам структуры класса, таким как:
>- Поля (`getFields()`, `getDeclaredField()`)
>- Методы (`getMethods()`, `getDeclaredMethod()`)
>- Конструкторы (`getConstructors()`, `getDeclaredConstructor()`)
>- Суперклассы (`getSuperclass()`)
>- Интерфейсы (`getInterfaces()`)

##### **Взаимодействие с `ClassLoader`**
- Метод `getClass()` возвращает объект `Class`, который связан с загрузчиком класса (`ClassLoader`).
- Если два класса с одинаковым именем загружены разными загрузчиками, они будут считаться разными.

![[Снимок экрана 2025-01-27 в 16.31.38.png|700]]
- `instanceof` проверяет принадлежность объекта к классу или его наследникам, 
- а `getClass()` требует точного соответствия классу.

### **Вывод**
Метод **`getClass()`** — это мощный инструмент для анализа классов объектов, строгого сравнения типов и использования рефлексии. Он незаменим, когда важна точность определения класса, и обеспечивает надёжность благодаря невозможности переопределения.











[^1]:Сигнатура метода `getClass()`
	=
	
	```java
	public final native Class<?> getClass();
	```
	
	- **`public`** — метод доступен везде.
	- **`final`** — метод нельзя переопределить в подклассах, что гарантирует консистентность его поведения.
	- **`native`** — метод реализован на уровне JVM, а не в Java-коде.
	- Возвращает объект типа `Class<?>`, который представляет класс текущего объекта.

[^2]:У каждого класса в Java есть только один объект `Class`. (Этот объект создаётся автоматически и хранится в памяти. Все вызовы `getClass()` для объектов одного класса возвращают один и тот же объект `Class`.)
	**Пример:**
	```java
	class Person {}
	public class Main {
	    public static void main(String[] args) {
	        Person p1 = new Person();
	        Person p2 = new Person();
	
	        System.out.println(p1.getClass() == p2.getClass()); // true
	    }
	}
	```
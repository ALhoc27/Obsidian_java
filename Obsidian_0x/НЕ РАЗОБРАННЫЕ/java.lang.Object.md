Класс `java.lang.Object` является корневым классом всей иерархии классов в Java. Каждый класс в Java, явным образом или неявно, расширяет класс `Object`. Таким образом, все классы автоматически наследуют методы, определенные в этом классе.
`java.lang.Object` предоставляет базовые методы, которые могут быть переопределены, чтобы кастомизировать их поведение для пользовательских классов.

***Общая структура класса*** `Object`
```java
public class Object {
    public Object();
    protected Object clone() throws CloneNotSupportedException;
    public boolean equals(Object obj);
    protected void finalize() throws Throwable;
    public final Class<?> getClass();
    public int hashCode();
    public String toString();
    public void notify();
    public void notifyAll();
    public void wait() throws InterruptedException;
    public void wait(long timeout) throws InterruptedException;
    public void wait(long timeout, int nanos) throws InterruptedException;
}
```
## Методы:
### `clone()`  - Создает и возвращает копию текущего объекта.
Метод **`clone()`** в Java позволяет создавать копию объекта. Этот метод является частью класса `java.lang.Object` и должен быть переопределен, если вы хотите использовать его для создания глубоких или поверхностных копий объектов.
#### Сигнатура:
```java
protected Object clone() throws CloneNotSupportedException;
```
#### Описание:
- **`protected`**: Метод имеет модификатор доступа `protected`, поэтому его нельзя вызвать напрямую на объекте из другого пакета, если не переопределить метод с более широким доступом (например, `public`).[^500]
- **Исключение**: Если класс не реализует интерфейс `Cloneable`, будет выброшено исключение `CloneNotSupportedException`.

- **Интерфейс `Cloneable`:**
	- Для использования метода `clone()` объект должен принадлежать классу, который реализует интерфейс `Cloneable`.
	- **`Cloneable`** – это маркерный интерфейс, то есть он не содержит методов. Его реализация служит сигналом JVM, что объект поддерживает клонирование.

- **Тип клонирования:**
	    - **Поверхностное клонирование (Shallow Copy):** По умолчанию `clone()` выполняет побитовое копирование объекта. Для ссылочных типов внутри объекта копируются только ссылки, а не сами объекты.
	    - **Глубокое клонирование (Deep Copy):** Чтобы создать полную копию объекта, включая вложенные объекты, нужно вручную реализовать глубокое клонирование.

***Пример***
```java
class MyClass implements Cloneable {
    int data;

    public MyClass(int data) {
        this.data = data;
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}

MyClass obj1 = new MyClass(10);
MyClass obj2 = (MyClass) obj1.clone();
```

<table class="language-java_td" style="width: 99%; border-collapse: collapse; margin-bottom: 5px;">
	<tr>
		<strong style="font-size: 1.1em; color: #333;">Примеры глубокого и поверхностного копирования объектов :</strong>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333;"><span style="border: 1px solid black; padding: 2px;">#1</span>
&nbsp; Поверхностное копирование (Shallow Copy):</strong>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333;"><span style="border: 1px solid black; padding: 2px;">#2</span>
&nbsp; Глубокое копирование (Deep Copy):</strong>
        </td>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">При поверхностном копировании создается новый объект, но вложенные объекты копируются как ссылки. То есть, изменения в вложенных объектах одного экземпляра будут видны в другом.
            <pre class="language-java_td" style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
class Address implements Cloneable {
    String city;
 
    public Address(String city) {
        this.city = city;
    }
 
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}
 
class Person implements Cloneable {
    String name;
    Address address;
 
    public Person(String name, Address address) {
        this.name = name;
        this.address = address;
    }
 
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone(); // Стандартное поверхностное копирование
    }
}
 
public class Main {
    public static void main(String[] args) throws CloneNotSupportedException {
        Address address = new Address("New York");
        Person person1 = new Person("John", address);
 
        // Поверхностное копирование
        Person person2 = (Person) person1.clone();  // person1.clone() - возвращает обьект типа Object 
 
        // Изменение в вложенном объекте
        person2.address.city = "Los Angeles";
 
        System.out.println(person1.address.city); // Вывод: Los Angeles
        System.out.println(person2.address.city); // Вывод: Los Angeles
    }
}
				</code>
            </pre>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">При глубоком копировании создается новый объект, включая вложенные объекты. То есть, изменения в вложенных объектах одного экземпляра не повлияют на другой.
            <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
class Address implements Cloneable {
    String city;
 
    public Address(String city) {
        this.city = city;
    }
 
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone(); // Клонирование объекта Address
    }
}
 
class Person implements Cloneable {
    String name;
    Address address;
 
    public Person(String name, Address address) {
        this.name = name;
        this.address = address;
    }
 
    @Override
    protected Object clone() throws CloneNotSupportedException {
        Person clonedPerson = (Person) super.clone();
        clonedPerson.address = (Address) address.clone(); // Глубокое клонирование вложенного объекта
        return clonedPerson;
    }
}
 
public class Main {
    public static void main(String[] args) throws CloneNotSupportedException {
        Address address = new Address("New York");
        Person person1 = new Person("John", address);
 
        // Глубокое копирование
        Person person2 = (Person) person1.clone();
 
        // Изменение в вложенном объекте
        person2.address.city = "Los Angeles";
 
        System.out.println(person1.address.city); // Вывод: New York
        System.out.println(person2.address.city); // Вывод: Los Angeles
    }
}
				</code>
            </pre>
        </td>
    </tr>
</table>

###### Подробнее <span style="border: 1px solid black; padding: 2px; line-height: 1.75;">#1</span>: &nbsp; <br/>
- В этом случае поле `address` в объекте `person1` и `person2` указывает на один и тот же объект в памяти.
- Поэтому изменения в поле `address.city` для `person2` отразятся в `person1`.
###### Подробнее <span style="border: 1px solid black; padding: 2px; line-height: 1.75;">#2</span>: &nbsp; <br/>
- В этом случае поле `address` клонируется в отдельный объект с помощью вызова `address.clone()`.
- Таким образом, изменения в `person2.address` не затрагивают `person1.address`.
#### Сравнения

![[Снимок экрана 2024-12-22 в 01.47.56.png|750]]

#### **Недостатки метода `clone()`**
1. **Сложность глубокого клонирования:**
    - Для сложных объектов реализация глубокого клонирования может стать трудоемкой.
2. **Устаревший подход:**
    - Многие разработчики избегают использования `clone()`, предпочитая создавать методы для ручного копирования (например, конструкторы копирования или статические фабрики).
3. **Маркерный интерфейс `Cloneable`:**
    - Интерфейс `Cloneable` не предоставляет четкого контракта для глубокого клонирования, что может приводить к ошибкам.

#### **Альтернативы методу `clone()`**
1. **Конструктор копирования:**
```java
class Person {
    String name;
    Address address;

    public Person(String name, Address address) {
        this.name = name;
        this.address = address;
    }

    // Конструктор копирования
    public Person(Person original) {
        this.name = original.name;
        this.address = new Address(original.address.city);
    }
}
```
2. **Сериализация/Десериализация:**
```java
// Использование ObjectOutputStream и ObjectInputStream для создания копий
```
3. **Библиотеки для клонирования:**
- `Apache Commons Lang`: класс `SerializationUtils` поддерживает глубокое клонирование.
#### **Заключение**
Метод `clone()` — это удобный инструмент для быстрого копирования объектов, но его использование требует внимания к деталям, особенно при работе с вложенными объектами. Хотя он остается полезным для простых случаев, альтернативы вроде конструкторов копирования часто предпочтительнее для сложных структур.


### equals(Object obj): - Cравнивают объекты на логическое равенство. [^101] 
Метод **`equals(Object obj)`** в Java используется для сравнения объектов на логическое равенство. Этот метод определен в классе **`Object`**, и каждая Java-класс наследует его. Однако поведение метода по умолчанию часто переопределяется для классов, где требуется сравнение содержимого, а не ссылок. По умолчанию этот метод сравнивает две ссылки на объекты, используя оператор `==`, то есть два объекта считаются равными, если они указывают на одно и то же место в памяти.
#### Сигнатура метода:
```java
public boolean equals(Object obj);
```
- **Параметр `obj`**: Объект, с которым сравнивается текущий объект.
- **Возвращаемое значение**: `true`, если объекты равны; `false` в противном случае.
	
**Переопределение:** В большинстве случаев разработчики переопределяют этот метод, чтобы сравнивать содержимое объектов, а не их адреса в памяти. 
#### Поведение по умолчанию
По умолчанию реализация метода `equals()` из класса `Object` проверяет **ссылочное равенство**, то есть, являются ли два объекта одной и той же областью памяти:
```java
public boolean equals(Object obj) {
    return (this == obj);
}
```
- **`this == obj`**: Возвращает `true`, если переменные `this` и `obj` указывают на один и тот же объект.
#### Сравнение ссылок:
```java
class Test {
    int value;

    Test(int value) {
        this.value = value;
    }
}

public class Main {
    public static void main(String[] args) {
        Test obj1 = new Test(10);
        Test obj2 = new Test(10);

🔵        System.out.println(obj1.equals(obj2)); // false (по умолчанию сравниваются ссылки)
    }
}
```

***Пример `equals()` с подробными комментариями:***
```java
class Person {
    private String name; 
    private int age;     

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Переопределяем метод equals()
    @Override
    public boolean equals(Object obj) {
        // Шаг 1: Проверяем, сравниваем ли объект сам с собой
⚫️        if (this == obj) {
            return true; // Если ссылки одинаковы, объекты равны
        }

        // Шаг 2: Проверяем, что сравниваемый объект не null и принадлежит тому же классу
🟠        if (obj == null || getClass() != obj.getClass()) {
            return false; // Если другой объект null или его класс отличается, они не равны
        }

        // Шаг 3: Приводим объект к типу Person, чтобы можно было сравнить поля
        Person person = (Person) obj;

        // Шаг 4: Сравниваем поля name и age
        // Для строки используем метод equals(), так как это объект
🔴        return age == person.age && (name != null ? name.equals(person.name) : person.name == null);
    }

    // Переопределяем toString() для наглядного вывода объекта
    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + "}";
    }
}

public class Main {
    public static void main(String[] args) {
        // Создаем два объекта с одинаковыми значениями полей
        Person p1 = new Person("Alice", 30);
        Person p2 = new Person("Alice", 30);

        // Создаем объект с отличающимся полем
        Person p3 = new Person("Bob", 25);

        // Проверяем равенство объектов
        System.out.println(p1.equals(p2)); // true: p1 и p2 имеют одинаковые поля
        System.out.println(p1.equals(p3)); // false: p1 и p3 отличаются
        System.out.println(p1.equals(null)); // false: p1 не равен null
    }
}
```
#### **Подробный разбор кода**
1. **Проверка на ссылочное равенство:**
```java
if (this == obj) {
    return true;
}
```
Это быстрый способ определить, что два объекта равны, если они указывают на одну область памяти. Пример [^499]
2. **Проверка на `null` и сравнение классов:**
```java
if (obj == null || getClass() != obj.getClass()) {
    return false;
}
```
- Если `obj == null`, то объект не может быть равен текущему объекту.
- `getClass()` используется для проверки, принадлежат ли оба объекта одному классу.  
    Это важно, чтобы избежать ошибок приведения типов.
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
">Важно: если класс-наследник участвует в сравнении объектов с использованием метода <code>equals()</code>, подход с проверкой <code>getClass() != obj.getClass()</code> может быть слишком строгим, поскольку он требует, чтобы объекты имели <b>точно тот же класс</b>, исключая наследников. В таких случаях лучше использовать более гибкий подход, например, проверку с помощью оператора <code>instanceof</code>. [[instanceof()]]
</dir>
1. 




#### **Когда переопределять метод `equals()`**
Переопределять метод `equals()` нужно, если:
1. **Вы хотите сравнивать содержимое объектов, а не ссылки.**
2. **Класс представляет сущности с логическим определением равенства** (например, `Person`, `Rectangle`).

#### **Рекомендации при переопределении `equals()`**
1. **Симметричность**: Если `x.equals(y)` возвращает `true`, то `y.equals(x)` также должно возвращать `true`.
```

```
1. **Рефлексивность**: Для любого ненулевого объекта `x`, вызов `x.equals(x)` должен возвращать `true`.
2. **Транзитивность**: Если `x.equals(y)` и `y.equals(z)` возвращают `true`, то `x.equals(z)` также должно возвращать `true`.
3. **Непротиворечивость**: Многократные вызовы `x.equals(y)` должны возвращать один и тот же результат, пока объекты не изменятся.
4. **Сравнение с `null`**: Любой объект должен быть неравен `null`. То есть `x.equals(null)` всегда возвращает `false`.


[^500]:Чтобы использовать метод `clone()` в других пакетах, его можно переопределить с модификатором доступа **`public`**:
	```java
	class MyClass implements Cloneable {
	    private int value;
	
	    public MyClass(int value) {
	        this.value = value;
	    }
	
	    @Override
	    public Object clone() throws CloneNotSupportedException {
	        return super.clone(); // Вызов родительского метода
	    }
	
	    @Override
	    public String toString() {
	        return "MyClass{value=" + value + "}";
	    }
	}
	
	public class Main {
	    public static void main(String[] args) throws CloneNotSupportedException {
	        MyClass obj1 = new MyClass(42);
	        MyClass obj2 = (MyClass) obj1.clone();
	
	        System.out.println(obj1); // MyClass{value=42}
	        System.out.println(obj2); // MyClass{value=42}
	    }
	}
	```
	Теперь метод `clone()` доступен извне, и объект может быть клонирован.
	
	### ==Пример ограничения доступа (если не сделать метод `public`)==
	Если метод `clone()` не переопределен или переопределен, но оставлен `protected`, следующий код вызовет ошибку компиляции, если доступ идет из другого пакета:
	```java
	package pkg1;
	
	public class MyClass implements Cloneable {
	    @Override
	    🔴 protected Object clone() throws CloneNotSupportedException {
	        return super.clone();
	    }
	}
	
	package pkg2;
	
	import pkg1.MyClass;
	
	public class Main {
	    public static void main(String[] args) throws CloneNotSupportedException {
	        MyClass obj1 = new MyClass();
	        MyClass obj2 = (MyClass) obj1.clone(); // Ошибка компиляции: clone() has protected access
	    }
	}
	```
	### Итог:
	Если вы хотите разрешить вызов `clone()` для объектов вашего класса извне, **переопределите его с модификатором доступа `public`**.


[^499]:```java
	Person p1 = new Person("Alice", 30);
	Person p2 = p1;
	System.out.println(p1.equals(p2)); 🟠 // true 
	```
[^101]:
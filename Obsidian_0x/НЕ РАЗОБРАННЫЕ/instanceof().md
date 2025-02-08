- *[[getClass()]]*

Оператор `instanceof` в Java — это бинарный оператор[^7], который используется для проверки принадлежности объекта к определенному классу или интерфейсу. Этот оператор помогает определять, является ли объект экземпляром конкретного класса или его подтипа.
#### Синтаксис [^5]
```java
object instanceof ClassName
```
- `object` — объект, который проверяется.
- `ClassName` — класс или интерфейс, на соответствие которому проверяется объект.
- Возвращает:
    - `true`, если объект является экземпляром указанного класса или его подкласса (или реализует интерфейс).
    - `false` в противном случае.

###### **Пример:** *проверка принадлежности объекта к классу*
```java
String str = "Hello, World!";
System.out.println(str instanceof String); // true
```

###### **Пример:** *проверка принадлежности к подклассу*
```java
class Animal {}
class Dog extends Animal {}

public class Main {
    public static void main(String[] args) {
        Animal animal = new Animal();
        Dog dog = new Dog();

        // Проверяем типы
        System.out.println(dog instanceof Animal); // true, Dog является подклассом Animal
        System.out.println(animal instanceof Dog); // false, Animal не является Dog
        System.out.println(dog instanceof Dog);    // true, объект dog — это Dog

		Animal ad = new Dog(); // Переменная типа Animal ссылающаяся на обьект класса Dog
		System.out.println(a instanceof Animal); // true 
		System.out.println(a instanceof Dog); // true
    }
}
```

> [!NOTE] Важно
> Проверка основана на фактическом типе объекта, а не на типе переменной, которая ссылается на объект.
>```java
Animal ad = new Dog(); // Переменная типа Animal ссылающаяся на обьект класса Dog
System.out.println(a instanceof Animal); // true 
System.out.println(a instanceof Dog); // true
> ```
> Фактический тип обьекта переменной `ad` имеет тип  `Dog` 
> - `Dog` является подклассом `Animal` // значит `true` 
> - `Dog` является классом `Dog` // значит `true` 



<table class="language-java_td" style="width: 99%; border-collapse: collapse; margin-bottom: 5px;">
	<tr>
		<strong style="font-size: 1.1em; color: #333;">Еще примеры :</strong>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333; line-height: 1.7;"><span style="border: 1px solid black; padding: 2px;">#1</span>
&nbsp; 1. Проверка интерфейсов</strong><br/>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333; line-height: 1.7;"><span style="border: 1px solid black; padding: 2px;">#2</span>
&nbsp; 2. Проверка принадлежности к подклассу<br/></strong>
        </td>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre class="language-java_td" style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
interface Playable {}
class Toy implements Playable {}
 
public class Main {
    public static void main(String[] args) {
		Playable p = new Toy();
		System.out.println(p instanceof Playable); // true
		System.out.println(p instanceof Toy);      // true
		}
}
				</code>
            </pre>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
class Animal {
    void sound() {
        System.out.println("Some sound");
    }
}
 
class Dog extends Animal {
    void sound() {
        System.out.println("Bark");
    }
}
 
class Cat extends Animal {
    void sound() {
        System.out.println("Meow");
    }
}
 
public class Main {
    public static void main(String[] args) {
        Animal a = new Dog();
 
🟤      if (a instanceof Dog) {
            Dog d = (Dog) a; // Безопасное приведение
            d.sound(); // Bark
        }
    }
}
				</code>
            </pre>
        </td>
    </tr>
    <tr>
	    <td>Объект <code>p</code> одновременно принадлежит и интерфейсу <code>Playable</code>, и классу <code>Toy</code>.
	    </td>
	    <td>🟤<br> <b>-</b> Оператор <code>instanceof</code> проверяет, является ли объект, на который ссылается <code>a</code>, экземпляром класса <code>Dog</code> (или его подкласса).<br>
	    <b>-</b> В данном случае, <code>a</code> указывает на объект <code>Dog</code>, поэтому результат проверки — <code>true</code>.
	    </td>
    </tr>
</table>

> [!WARNING] Как уже говорилось `instanceof` проверка основана **на фактическом типе объекта**
> - В примере 🟤, `Animal a = new Dog();` переменная `a` - является обьектом типа `Dog`
>   Поэтому `a instanceof Dog` вернет `true`
>```java
>if (a instanceof Dog) {
 >	Dog d = (Dog) a; // Безопасное приведение
 >	d.sound(); // Bark
}
>```
>Данный код безопасный, потому что в случае если переменная `a` - не является классом `Dog` или его подтипом, он просто не выполнится 



> [!NOTE] Не требуется проверять на `null`
> - Оператор проверяет тип объекта(*всю иерархию классов*) **на момент выполнения программы** (runtime).
> - Если объект равен `null`, `instanceof`[^10] всегда возвращает `false` ==не требуется проверять на `null`== как у `getClass()` [^6]

### **Ключевые особенности**
1. **Для объекта `null` результат всегда `false`: 
	- Если объект равен `null`, `instanceof` всегда возвращает `false` ==не требуется проверять на `null`== как у `getClass()` [^6])
```java
String str = null;
System.out.println(str instanceof String); // false
```
2. **Поддержка наследования:**
	- Если объект является экземпляром подкласса, то `instanceof` вернёт `true` для суперкласса.
```java
class Animal {}
class Dog extends Animal {}

Animal a = new Dog();
System.out.println(a instanceof Animal); // true
```
3. **Проверка интерфейсов и абстрактных классов:**
	- Если объект реализует интерфейс, `instanceof` вернёт `true`.
```java
interface Runnable {}
class Task implements Runnable {}

Task task = new Task();
System.out.println(task instanceof Runnable); // true
```
4. **Безопасное приведение типов** (*нельзя использовать `instanceof` с несовместимыми типами*):
	- Используется перед приведением типов, чтобы убедиться, что объект принадлежит нужному классу и избежать ошибок времени выполнения (`ClassCastException`).
	```java
	Object obj = "Hello";
	if (obj instanceof String) {
	    String str = (String) obj; // Безопасное приведение типа
	    System.out.println(str);
	}
	```
	*Но вообще сейчас есть джинерики и лучше использовать вполне конкретную типизацию.*
	- Если классы находятся в разных ветвях иерархии, компилятор выдаст ошибку:
```java
class Animal {}
class Car {}

Animal a = new Animal();
System.out.println(a instanceof Car); // Ошибка компиляции
```

##### **Пример использования в `equals`**
Оператор `instanceof` может использоваться в методе `equals()`, чтобы проверить, что объект принадлежит текущему классу или его подклассу.
```java
class Person {
    private String name;

    public Person(String name) {
        this.name = name;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) {
            return true; // Сравнение по ссылке
        }
🔵      if (!(obj instanceof Person)) {
            return false; // Если объект не является Person
        }
        Person other = (Person) obj;
        return name != null ? name.equals(other.name) : other.name == null;
    }
}
```

> [!NOTE]
> 
> #### Различие между `instanceof` и `getClass()`: [^9]
> ![[Снимок экрана 2024-12-24 в 02.03.03.png|750]]
> - **`getClass() != obj.getClass()`**
>
>   - Проверяет, чтобы классы объектов совпадали точно.
>   - Используется, если логика равенства должна быть строго ограничена одним классом (без учета наследников).
> - **`instanceof`**
>     - Проверяет, является ли объект экземпляром текущего класса или его подкласса.
>     - Используется, если требуется поддержка наследования в логике равенства.

<table class="language-java_td" style="width: 99%; border-collapse: collapse; margin-bottom: 5px;">
	<tr>
		<strong style="font-size: 1.1em; color: #333;">Пример <code>getClass()</code> и <code>instanceof</code>:</strong>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333;"><span style="border: 1px solid black; padding: 2px;">#1</span>
&nbsp; Пример с использованием <code>getClass()</code>:</strong>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333;"><span style="border: 1px solid black; padding: 2px;">#2</span>
&nbsp; Пример с использованием <code>instanceof</code>:</strong>
        </td>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre class="language-java_td" style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
class Person {
    private String name;
 
    public Person(String name) {
        this.name = name;
    }
 
    @Override
    public boolean equals(Object obj) {
        if (this == obj) {
            return true; // Проверка ссылочного равенства
        }
🟠        if (obj == null || getClass() != obj.getClass()) {
            return false; // Классы должны совпадать точно
        }
        Person person = (Person) obj;
        return name != null ? name.equals(person.name) : person.name == null;
    }
}
 
class Employee extends Person {
    private String company;
 
    public Employee(String name, String company) {
        super(name);
        this.company = company;
    }
}
 
public class Main {
    public static void main(String[] args) {
        Person p = new Person("Alice");
        Employee e = new Employee("Alice", "TechCorp");
 
        System.out.println(p.equals(e)); // false, так как классы разные
        System.out.println(e.equals(p)); // false, так как классы разные
    }
}
				</code>
            </pre>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd;"> Если вам нужно поддерживать наследников в сравнении:
            <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
class Person {
    private String name;
  
    public Person(String name) {
        this.name = name;
    }
  
    @Override
    public boolean equals(Object obj) {
        if (this == obj) {
            return true; // Проверка ссылочного равенства
        }
🟡        if (obj instanceof Person) { // Проверка на null не требуется
            return false; // Проверяем, что объект является экземпляром Person или его подкласса
        }
        Person person = (Person) obj;
🔵      return name != null ? name.equals(person.name) : person.name == null;
    }
}
  
class Employee extends Person {
    private String company;
   
    public Employee(String name, String company) {
        super(name);
        this.company = company;
    }
}
   
public class Main {
    public static void main(String[] args) {
        Person p = new Person("Alice");
        Employee e = new Employee("Alice", "TechCorp");
  
        System.out.println(p.equals(e)); // true, так как поля name совпадают
        System.out.println(e.equals(p)); // true, так как поля name совпадают
    }
}
				</code>
            </pre>
        </td>
    </tr>
</table>

###### Подробнее <span style="border: 1px solid black; padding: 2px; line-height: 1.75;">#1</span>: &nbsp; <br/>
- 🟠 ==***Используется для проверки, что:***== 
	- Если объект `obj` равен `null` или у объекта на котором вызывается метод `equals()` тип отличается с обьектом передаваемым аргументом, **то** `equals()` **вернет** `FALSE`

###### Подробнее <span style="border: 1px solid black; padding: 2px; line-height: 1.75;">#2</span>: &nbsp; <br/>
- 🟡 ==***Используется для проверки, что:***== 
	- ** объект `obj` имеет **тот же класс**(тип) **или является** классом(типом) **наследником**
- 🔵 Эта строка проверяет, равны ли значения полей `name` текущего объекта (`this`) и другого объекта (`person`), с учётом возможного значения `null`. [^8]
	- Если поле `name` текущего объекта ( `this.name` ) равно `null`, проверяется, равно ли поле `name` объекта `person` также `null`.

> [!WARNING] Используя `instanceof` проверка на `null`  **не требуется**
> - Когда вы используете **`instanceof`**, проверка на `null`  **не требуется**, так как `instanceof` уже выполняет эту проверку.
>```java
> if (!(obj instanceof Person)) { 
> 	return false; // Проверяем, что объект является экземпляром Person или его подкласса 
> }
>```
>**Оператор `instanceof` проверяет, принадлежит ли объект `obj` классу `Person` или его потомкам.**
>&nbsp;&nbsp;&nbsp;&nbsp; - Если объект не является экземпляром `Person`, то логически он не может быть "равным" текущему объекту.
#### **Контракт `equals()` и проблемы с наследованием** 
> - [[Контракт метда 'equals()']]
> - [[boolean equals(Object obj)]]
> 
> Использование `instanceof` вместо `getClass()` в методе `equals()` делает сравнение более гибким, но может нарушить **симметричность**:
> ```java
> class Person {
>     private String name;
> 
>     public Person(String name) {
>         this.name = name;
>     }
> 
>     @Override
>     public boolean equals(Object obj) {
>         if (this == obj) return true; // Рефлексивность
>         if (obj instanceof Person) {  // Проверка через instanceof
>             Person other = (Person) obj;
>             return name.equals(other.name);
>         }
>         return false;
>     }
> }
> 
> class Employee extends Person {
>     private int employeeId;
> 
>     public Employee(String name, int employeeId) {
>         super(name);
>         this.employeeId = employeeId;
>     }
> }
> ```
> ##### Сценарий нарушения симметричности:
> ```java
> Person person = new Person("Alice");
> Employee employee = new Employee("Alice", 123);
> 
> System.out.println(person.equals(employee)); // true (Person видит Employee как Person)
> System.out.println(employee.equals(person)); // false (Employee требует точного совпадения типов)
> ```
> 


> | ![[Снимок экрана 2025-01-27 в 15.52.52.png\|500]] | ![[Снимок экрана 2025-01-27 в 15.53.19.png\|500]] |
> | ------------------------------------------------- | ------------------------------------------------- |
> ![[Снимок экрана 2025-01-27 в 15.55.34.png|600]]

<br/><div style="text-align: center; margin: 0; padding: 0;"> <span style="color: #ff7e5f; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> <span style="color: #feb47b; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> <span style="color: #4facfe; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> </div>

[^1]:```java
	class Person {
	    private String name;
	
	    public Person(String name) {
	        this.name = name;
	    }
	
	    @Override
	    public boolean equals(Object obj) {
	        if (this == obj) {
	            return true; // Проверка ссылочного равенства
	        }
	🟣      if (obj == null || getClass() != obj.getClass()) {
	            return false; // Классы должны совпадать точно
	        }
	        Person person = (Person) obj;
	        return name != null ? name.equals(person.name) : person.name == null;
	    }
	}
	
	class Employee extends Person {
	    private String company;
	
	    public Employee(String name, String company) { // 
	        super(name);
	        this.company = company;
	    }
	}
	
	public class Main {
	    public static void main(String[] args) {
	        Person p = new Person("Alice");
	        Employee e = new Employee("Alice", "TechCorp");
	
	🟤      System.out.println(p.equals(e)); // false, так как классы разные
	🟤      System.out.println(e.equals(p)); // false, так как классы разные
	    }
	}
	```
	#### **Объяснение:**
	- 🟤 Здесь сравнение объектов класса `Person` и `Employee` вернет `false`, их классы разные.


[^5]:![[Снимок экрана 2025-01-24 в 11.06.08.png]]

[^6]:![[Снимок экрана 2025-01-24 в 16.31.36.png]]

[^7]:![[Снимок экрана 2025-01-27 в 13.25.04.png|600]]
	##### Пример
	```java
	String str = "Hello, world!";
	System.out.println(str instanceof String); // true
	```
	- Левый операнд: `str` (объект).
	- Правый операнд: `String` (класс).
	- Результат: `true`, потому что объект `str` принадлежит классу `String`.

[^8]:![[Снимок экрана 2025-01-27 в 15.32.41.png|550]]

[^9]:![[Снимок экрана 2025-01-27 в 15.48.12.png|550]]

[^10]:![[Снимок экрана 2025-01-28 в 20.46.21.png]]
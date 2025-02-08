**Симметричность** — это свойство метода `equals()` в Java, которое требует, чтобы результат сравнения двух объектов был одинаковым, независимо от того, с какой стороны производится вызов.

> [!Правило]
> **Иными словами:**  
> Если `x.equals(y)` возвращает `true`, то вызов `y.equals(x)` также должен возвращать `true`.
> **Аналогично:**  
> Если `x.equals(y)` возвращает `false`, то вызов `y.equals(x)` также должен возвращать `false`.

***Пример корректного соблюдения Симметричности***
```java
class Person {
	private String name;

	public Person(String name) {
		this.name = name;
	}

	@Override
	public boolean equals(Object obj) {
		if (this == obj) return true; // Сравнение с самим собой
		if (obj == null || getClass() != obj.getClass()) return false; // Проверка на null и класс
		Person other = (Person) obj;
		return this.name.equals(other.name); // Сравнение значимого поля
	}
}

public class Main {
	public static void main(String[] args) {
		Person p1 = new Person("Alice");
		Person p2 = new Person("Alice");

		// Симметричность соблюдена:
		System.out.println(p1.equals(p2)); // true
		System.out.println(p2.equals(p1)); // true
	}
}
```

<table class="language-java_td" style="width: 99%; border-collapse: collapse; margin-bottom: 5px;">
	<tr>
		<strong style="font-size: 1.1em; color: #333;">Пример :</strong>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333; line-height: 1.7;"><span style="border: 1px solid black; padding: 2px;">#1</span>
&nbsp; Пример нарушения Симметричности</strong>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333; line-height: 1.7;"><span style="border: 1px solid black; padding: 2px;">#2</span>
&nbsp; Исправленный код (c заменой на <code>getClass()</code>):</strong>
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
        if (this == obj) return true; // Сравнение ссылок  
🟣		if (obj instanceof Person) {  // Проверка на принадлежность к классу Person и его потомкам
            Person other = (Person) obj;  
            return name.equals(other.name); // Сравнение значимого поля name  
        }  
        return false;  
    }
     
	@Override 
🔵	public int hashCode() {
	     return name.hashCode(); // Хэш-код на основе поля name 
     }  
}  
    
class ExtendedPerson extends Person {  
    private int age;  
  
    public ExtendedPerson(String name, int age) {  
        super(name);  
        this.age = age;  
    }  
   
    @Override  
    public boolean equals(Object obj) {  
        if (this == obj) return true; // Сравнение ссылок  
🟤		if (getClass() != obj.getClass()) return false; // Строгая роверка на принадлежность только к одному и тому же классу 
        ExtendedPerson other = (ExtendedPerson) obj;  
🔴		return super.equals(other) && this.age == other.age; // Сравнение полей суперкласса и age  
    }  
  
🔵	@Override public int hashCode() { 
		return 31 * super.hashCode() + age; // Хэш-код на основе суперкласса и поля age 
	}
}  
  
public class Main {  
    public static void main(String[] args) {  
        Person p1 = new Person("Alice");  
        ExtendedPerson p2 = new ExtendedPerson("Alice", 25);  
  
        // Нарушение симметричности:  
        System.out.println("p1.equals(p2): " + p1.equals(p2)); // true  
        System.out.println("p2.equals(p1): " + p2.equals(p1)); // false  (для выполнения правила симмитричности должно быть true) 
    }  
}
				</code>
            </pre>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
class Person {
    private String name;
  
    public Person(String name) {
        this.name = name;
    }
  
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true; // Сравнение ссылок
        if (obj == null || getClass() != obj.getClass()) return false; // Проверка на точное совпадение классов
        Person other = (Person) obj;
        return name.equals(other.name); // Сравнение значимого поля name
    }
  
    @Override
🔵	public int hashCode() {
        return name.hashCode(); // Хэш-код на основе поля name
    }
}
  
class ExtendedPerson extends Person {
    private int age;
  
    public ExtendedPerson(String name, int age) {
        super(name);
        this.age = age;
    }
  
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true; // Сравнение ссылок
        if (obj == null || getClass() != obj.getClass()) return false; // Проверка на точное совпадение классов
        ExtendedPerson other = (ExtendedPerson) obj;
        return super.equals(other) && this.age == other.age; // Сравнение полей суперкласса и age
    }
  
🔵	@Override
    public int hashCode() {
        return 31 * super.hashCode() + age; // Хэш-код на основе поля name и age
    }
}
   
public class Main {
    public static void main(String[] args) {
        Person p1 = new Person("Alice");
        ExtendedPerson p2 = new ExtendedPerson("Alice", 25);
  
        // Проверка симметричности:
        System.out.println("Person.equals(ExtendedPerson): " + p1.equals(p2)); // false, потому что это разные классы
        System.out.println("ExtendedPerson.equals(Person): " + p2.equals(p1);  // false, потому что это разные классы
    }
}
				</code>
            </pre>
        </td>
    </tr>
</table>

###### Подробнее <span style="border: 1px solid black; padding: 2px; line-height: 1.75;">#1</span>: &nbsp; **Основная проблема в этом примере:**

 **==Нарушения симметричности==**:  
Контракт метода `equals()` требует, чтобы если `p1.equals(p2)` возвращает `true`, то `p2.equals(p1)` также возвращал `true`. Иными словами:  
`new Person("Alice").equals(new ExtendedPerson("Alice", 25))` **должен быть равен** `new ExtendedPerson("Alice", 25).equals(new Person("Alice"))`  

> У нас класс объекты `ExtendedPerson` могут сравниваться только с объектами того же класса(`getClass() != obj.getClass()`), а объекты класса `Person` с объектами того же класса но и со объектами классов наследников. (В этом и кроется нарушения симметричности) `Person` можно сравнить и с `Person`, и с `ExtendedPerson`, но `ExtendedPerson` только с `ExtendedPerson`.

 **Причины нарушения симметричности:**  
🟣 - В **классе `Person`** метод `equals()` **использует оператор `instanceof`**, что означает, что он проверяет принадлежность объекта к классу `Person` **или его подклассам**. (`Person` можно сравнить и с `Person`, и с `ExtendedPerson`)
🟤 - В **классе `ExtendedPerson`** метод `equals()` **использует `getClass()`**, который проверяет точное совпадение класса, исключая любые наследования. Это вызывает проблему при сравнении `Person` и `ExtendedPerson`, так как они не принадлежат одному и тому же классу. (`ExtendedPerson` можно сравнить только с `ExtendedPerson`)
🔴 - В **классе `ExtendedPerson`** при сравнении **используется `super.equals(other)`**, что позволяет сначала сравнить поля суперкласса `Person` (в данном случае только поле `name`), а затем проверять дополнительное поле `age`. 
==**`super.equals()` - означает вызов метода `equals()` из суперкласса текущего объекта (в данном случае, из класса, от которого наследуется текущий класс)**== [[super.equals(obj)]]
🔵 - **Переопределение `hashCode()`:** Для соблюдения контракта между `equals()` и `hashCode()` переопределен метод `hashCode()` в обоих классах.

- `Person` сравнивает только поле `name`, игнорируя класс объекта. Поэтому `p1.equals(p2)` возвращает `true`.
- `ExtendedPerson`, наследующий `Person`, имеет дополнительное поле `age`, и логика сравнения может учитывать его. Поэтому `p2.equals(p1)` возвращает `false`.<br/>
###### Подробнее <span style="border: 1px solid black; padding: 2px; line-height: 1.75;">#2</span>: &nbsp; **Исправление кода:**<br/>
В обоих классах (и в `Person`, и в `ExtendedPerson`) используется `getClass()` для точной проверки типов объектов. Это гарантирует, что объекты различных классов не будут сравниваться. Например, теперь объекты типа `Person` и `ExtendedPerson` не будут считаться равными, даже если они имеют одинаковые значения в полях `name`.
- **Исправление в классе `Person`:** В методе `equals()`, заменили `instanceof` на `getClass()` для проверки точного класса. Это позволит исключить все прочие классы и проверять только текущий.  

---
<table class="language-java_td" style="width: 99%; border-collapse: collapse; margin-bottom: 5px;">
	<tr>
		<strong style="font-size: 1.1em; color: #333;">Пример (с разрешением сравнений разных классов) :</strong>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333; line-height: 1.7;"><span style="border: 1px solid black; padding: 2px;">#1</span>
&nbsp; Пример нарушения Симметричности (тот же самый, что выше)</strong>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333; line-height: 1.7;"><span style="border: 1px solid black; padding: 2px;">#2</span>
&nbsp; Исправленный код (сравнение двух разных классов):</strong>
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
        if (this == obj) return true; // Сравнение ссылок  
🟣		if (obj instanceof Person) {  // Проверка на принадлежность к классу Person и его потомкам
            Person other = (Person) obj;  
            return name.equals(other.name); // Сравнение значимого поля name  
        }  
        return false;  
    }
     
	@Override 
🔵	public int hashCode() {
	     return name.hashCode(); // Хэш-код на основе поля name 
     }  
}  
    
class ExtendedPerson extends Person {  
    private int age;  
  
    public ExtendedPerson(String name, int age) {  
        super(name);  
        this.age = age;  
    }  
   
    @Override  
    public boolean equals(Object obj) {  
        if (this == obj) return true; // Сравнение ссылок  
🟤		if (getClass() != obj.getClass()) return false; // Строгая роверка на принадлежность только к одному и тому же классу 
        ExtendedPerson other = (ExtendedPerson) obj;  
🔴		return super.equals(other) && this.age == other.age; // Сравнение полей суперкласса и age  
    }  
  
🔵	@Override public int hashCode() { 
		return 31 * super.hashCode() + age; // Хэш-код на основе суперкласса и поля age 
	}
}  
  
public class Main {  
    public static void main(String[] args) {  
        Person p1 = new Person("Alice");  
        ExtendedPerson p2 = new ExtendedPerson("Alice", 25);  
  
        // Нарушение симметричности:  
        System.out.println("p1.equals(p2): " + p1.equals(p2)); // true  
        System.out.println("p2.equals(p1): " + p2.equals(p1)); // false  (для выполнения правила симмитричности должно быть true) 
    }  
}
				</code>
            </pre>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
class Person {  
    private String name;  
   
    public Person(String name) {  
        this.name = name;  
    }  
   
    @Override  
⚫️	public boolean equals(Object obj) {  
        if (this == obj) return true; // Сравнение ссылок  
        if (!(obj instanceof Person)) return false; // Проверяем, что объект — это тип Person или его подкласс  
        Person other = (Person) obj;  
        return name.equals(other.name);  
    }  
   
    @Override  
    public int hashCode() {  
        return name.hashCode(); // Хэш-код на основе поля name  
    }  
}  
   
class ExtendedPerson extends Person {  
    private int age;  
   
    public ExtendedPerson(String name, int age) {  
        super(name);  
        this.age = age;  
    }  
   
    @Override  
🟠	public boolean equals(Object obj) {  
        return super.equals(obj); // Сравнение базового и дополнительного поля age  
    }  
   
    @Override  
    public int hashCode() {  
        return 31 * super.hashCode() + age; // Хэш-код на основе суперкласса и age  
    }  
}  
   
public class Main {  
    public static void main(String[] args) {  
        Person p1 = new Person("Alice");  
        ExtendedPerson p2 = new ExtendedPerson("Alice", 25);  
        ExtendedPerson p3 = new ExtendedPerson("Al", 25);  
   
        // Проверка симметричности:  
        System.out.println("p1.equals(p2): " + p1.equals(p2)); // true (при том что разные классы, name одинаковое)  
        System.out.println("p2.equals(p1): " + p2.equals(p1)); // true (при том что разные классы, name одинаковое)  
   
        System.out.println("p1.equals(p3): " + p1.equals(p3)); // false (name разное)  
        System.out.println("p3.equals(p1): " + p3.equals(p1)); // false (name разное)  
   
        // Проверка рефлексивности:        System.out.println("p1.equals(p1): " + p1.equals(p1)); // true  
        System.out.println("p2.equals(p2): " + p2.equals(p2)); // true  
    }  
}
				</code>
            </pre>
        </td>
    </tr>
</table>

###### Подробнее <span style="border: 1px solid black; padding: 2px; line-height: 1.75;">#1</span>:   **Основная проблема в этом примере:**
 **==Нарушения симметричности==**:  
Контракт метода `equals()` требует, чтобы если `p1.equals(p2)` возвращает `true`, то `p2.equals(p1)` также возвращал `true`. Иными словами:  
`new Person("Alice").equals(new ExtendedPerson("Alice", 25))` **должен быть равен** `new ExtendedPerson("Alice", 25).equals(new Person("Alice"))`

> У нас класс объекты `ExtendedPerson` могут сравниваться только с объектами того же класса(`getClass() != obj.getClass()`), а объекты класса `Person` с объектами того же класса но и со объектами классов наследников. (В этом и кроется нарушения симметричности) `Person` можно сравнить и с `Person`, и с `ExtendedPerson`, но `ExtendedPerson` только с `ExtendedPerson`.

<br/>

###### Подробнее <span style="border: 1px solid black; padding: 2px; line-height: 1.75;">#2</span>: &nbsp; **Исправленный код (сравнение двух разных классов):**<br/>
> 🟠 В классе наследнике предопределен `equals()` следующим образом:
> ```java
> @Override  
> public boolean equals(Object obj) {  
> 	return super.equals(obj); // Сравнение базового и дополнительного поля age  
> }  
> ```
> ⚫️ Он ссылается на метод класса родителя:
> ```java
> @Override  
> public boolean equals(Object obj) {  
> 	if (this == obj) return true; // Сравнение ссылок  
> 	if (!(obj instanceof Person)) return false; // Проверяем, что объект — это тип Person или его подкласс  
> 	Person other = (Person) obj;  
> 	return name.equals(other.name);  
> }  
> ```
> То есть по сути, выполняется родительский метод 
---










#### ==**Основные способы достижения симметричности**==
##### 1. **Проверка класса объектов**
Чтобы сравнение было симметричным, важно убедиться, что оба объекта принадлежат одному и тому же классу. Это исключает ситуацию, когда один объект считает другой равным, а второй объект — нет.
Используются два подхода для проверки класса:
- **Проверка через `getClass()`**: Обеспечивает строгое равенство классов. [[getClass()]]
- **Проверка через `instanceof`**: Гибкая проверка, допускает наследование, но может нарушить симметричность [[instanceof()]]
##### 2. **Сравнение только значимых полей**
Симметричность нарушается, если два объекта используют разные поля для определения равенства. Чтобы избежать этого:
- Определите **набор значимых полей**, которые участвуют в сравнении и убедитесь, что оба объекта используют один и тот же набор полей. **Пример: [^3]**
##### 3. **Избегание использования `instanceof` для проверки класса**
Проверка через `instanceof` допускает сравнение объектов с использованием наследования, но может нарушить симметричность, если в наследуемом классе переопределена логика сравнения. (Как вы могли заметить в примерах выше)
##### 4. **Согласованная логика сравнения**
Симметричность также достигается за счет:
- Единообразного подхода к сравнению значений.
- Использования стандартных методов сравнения (например, `Objects.equals()`), чтобы исключить ошибки при работе с `null`.
Пример:[^2]
##### 6. **Не включайте в сравнение нестабильные или временные поля**
Поля, которые могут изменяться в процессе работы программы, могут нарушить симметричность. Например поля `id`

<br/><div style="text-align: center; margin: 0; padding: 0;"> <span style="color: #ff7e5f; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> <span style="color: #feb47b; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> <span style="color: #4facfe; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> </div>

[^1]:`super.equals(obj)` - ==**означает вызов метода `equals()` из суперкласса текущего объекта**== (в данном случае, из класса, от которого наследуется текущий класс). Это позволяет использовать реализацию метода `equals()` в суперклассе для сравнения тех полей, которые определены в этом суперклассе.
	
	Использование `super.equals()` в методе `equals()` класса `ExtendedPerson` имеет важное значение для правильного сравнения объектов, особенно в ситуации, когда класс `ExtendedPerson` является подклассом `Person`. 
	Вызов `super.equals()` позволяет выполнить сравнение полей, определённых в суперклассе (`Person`), перед тем как добавлять сравнение дополнительных полей (`age`) в подклассе (`ExtendedPerson`). Это упрощает логику и помогает избежать дублирования кода, который уже реализован в `equals()` суперкласса.
	### **Контекст вызова `super.equals(obj)`**
	Когда вы переопределяете метод `equals()` в подклассе, вам нужно учитывать поля как из суперкласса, так и из подкласса. Вместо того, чтобы повторно реализовывать логику сравнения полей суперкласса, вы вызываете `super.equals(obj)`.
	
	Этот вызов:
	1. Сравнивает те поля, которые определены в суперклассе.
	2. Возвращает результат (`true` или `false`) в зависимости от того, равны ли поля суперкласса.
	
	**Пример:**
	```java
	class Person {
	    private String name;
	
	    public Person(String name) {
	        this.name = name;
	    }
	
	    @Override
	    public boolean equals(Object obj) {
	        if (this == obj) return true; // Проверка на совпадение ссылок
	        if (obj == null || getClass() != obj.getClass()) return false; // Типы объектов не совпадают
	        Person other = (Person) obj;
	        return name.equals(other.name); // Сравнение поля name
	    }
	}
	
	class ExtendedPerson extends Person {
	    private int age;
	
	    public ExtendedPerson(String name, int age) {
	        super(name);
	        this.age = age;
	    }
	
	    @Override
	    public boolean equals(Object obj) {
	        if (this == obj) return true;
	        if (obj == null || getClass() != obj.getClass()) return false;
	
	        // Сравнение полей суперкласса через super.equals()
	        if (!super.equals(obj)) return false;
	
	        // Сравнение полей подкласса
	        ExtendedPerson other = (ExtendedPerson) obj;
	        return this.age == other.age;
	    }
	}
	```
	#### **Что происходит при вызове `super.equals(obj)`?**
	1. Если объект `obj` передан в метод `equals()` класса `ExtendedPerson`, сначала будет вызван метод `equals()` из `Person` через `super.equals(obj)`.
	2. Внутри `super.equals(obj)` происходит сравнение поля `name` между текущим объектом (`this`) и объектом `obj`.
	3. Если поля суперкласса равны, метод возвращает `true`, и выполнение продолжается для сравнения полей подкласса.
	4. Если поля суперкласса не равны, метод возвращает `false`, и дальнейшее сравнение прекращается.
	
	#### То есть:
	 1. **После проверок:**
	```java
	if (this == obj) return true;
	if (obj == null || getClass() != obj.getClass()) return false;
	```
	2. **Прежде выполнится(будет вызван метод супер класса):**
	```java
	// Сравнение полей суперкласса через super.equals()
	if (!super.equals(obj)) return false;
	```
	Метод супер класса (класса родитель `Person`):
	```java
	@Override
	public boolean equals(Object obj) {
		if (this == obj) return true; // Проверка на совпадение ссылок
		if (obj == null || getClass() != obj.getClass()) return false; // Типы объектов не совпадают
		Person other = (Person) obj;
		return name.equals(other.name); // Сравнение поля name
	}
	```
	Так как класс `Person`, класс родитель класса `ExtendedPerson` то без проблем `Person other = (Person) obj;` (проводится каст), и сравниваются поля, возвращая `true` / `false`
	
	> [!NOTE] Важно:
	>  `!super.equals(obj)` - вызов метода `equals()` из суперкласса ==**текущего объекта**== (то есть данный метод супер класса вызывается на текущем обьекте)
	>```java
	>public static void main(String[] args) {  
	 >   ExtendedPerson extendedPerson = new ExtendedPerson("sasa", 12);  
	>   ExtendedPerson extendedPerson1 = new ExtendedPerson("sasa", 12);  
	 >   System.out.println(extendedPerson.equals(extendedPerson1));  
	>}
	>```
	>Текущий обьект (пример выше), у нас `extendedPerson`, у него и вызывается метод `equals()` из суперкласса
	
	3. После сравнения полей супер класса, сравниваются поля на уровне под класса:
	```java
	// Сравнение полей подкласса
	ExtendedPerson other = (ExtendedPerson) obj;
	return this.age == other.age;
	```
	
	
	> [!TRIP] Важно помнить:
	>```java
	if (obj == null || getClass() != obj.getClass()) return false; // Типы объектов не совпадают
	>```
	> Что `getClass()` - не привязан какому то конкретному классу, этот метод возвращает класс текущего объекта (на котором вызывается данный метод).
	> **Выражение:**
	>```java
	>getClass() != obj.getClass()
	>```
	>Означает жесткую проверку, того что класс текущего обьекта равен классу `obj` (*обьект переданный аргументом методу `equals(obj)`*)
	> 
	
	
	
	

[^2]:##### 5. **Согласованная логика сравнения**
	Симметричность также достигается за счет:
	- Единообразного подхода к сравнению значений.
	- Использования стандартных методов сравнения (например, `Objects.equals()`), чтобы исключить ошибки при работе с `null`.
	```java
	@Override
	public boolean equals(Object obj) {
	    if (this == obj) return true;
	    if (obj == null || getClass() != obj.getClass()) return false;
	    MyClass other = (MyClass) obj;
	    return Objects.equals(this.field1, other.field1) && Objects.equals(this.field2, other.field2);
	}
	```

[^3]:**Пример:**
	```java
	class Person {
	    private String name;
	    private int age;
	
	    @Override
	    public boolean equals(Object obj) {
	        if (this == obj) return true;
	        if (obj == null || getClass() != obj.getClass()) return false;
	        Person other = (Person) obj;
	        return age == other.age && Objects.equals(name, other.name); // Используем одинаковые поля
	    }
	}
	```
- *[[Контракт метда 'equals()']]*
- *[[Objects.equals()]]*
- *[[instanceof()]]*
- *[[getClass()]]*
- *[[hashCode()]]*

Метод `boolean equals(Object obj)` – это важный метод в Java, который ==**определяет равенство двух объектов.**== Этот метод является методом класса `Object` и может быть переопределен в любом другом классе для обеспечения корректного сравнения объектов.
#### 1. **Сигнатура метода:**
```java
public boolean equals(Object obj)
```
- **Возвращаемое значение:**`true`, **если объект**, переданный в качестве аргумента, **равен текущему объекту**, иначе `false`.
- **Параметр:**`obj` – объект, с которым сравнивается текущий объект.
#### 2. Назначение метода `equals()`
> ==**Метод используется для проверки логического равенства двух объектов.**== По умолчанию, реализация в классе `Object` **сравнивает ссылки на объекты** (т.е., проверяет, указывают ли два объекта на одну и ту же область памяти)[^3].
#### **3. Стандартная реализация `equals()` в классе `Object`**
По умолчанию метод `equals()` в классе `Object` просто проверяет, ссылаются ли два объекта на одну и ту же область памяти. То есть, он возвращает `true`, если оба объекта являются одним и тем же объектом, а не двумя разными объектами с одинаковыми значениями полей.
###### Cтандартная реализации в классе Object:
```java
public boolean equals(Object obj) {
    return (this == obj); // Возвращает `true`, если оба объекта указывают на одну и ту же область памяти. 
}
```
По умолчанию `equals()` проверяет равенство ссылок. Но в реальных задачах часто требуется сравнивать содержимое объектов. 
#### 4. **Переопределение метода `equals()` [^4]**
Для того чтобы объекты могли сравнивать свои состояния, а не ссылки на них, необходимо переопределить метод `equals()` в своем классе. При этом важно следовать следующим правилам:
#### 5. **Основные правила переопределения equals()**
- **[[Рефлексивность (Reflexivity)]]**: `x.equals(x)` всегда должно быть `true`. 
- **[[Симметричность (Symmetry)]]**: Если `x.equals(y)`, то и `y.equals(x)` должно быть `true`.
- **[[Транзитивность (Transitivity)]]**: Если `x.equals(y)` и `y.equals(z)`, то `x.equals(z)` должно быть `true`.
- **[[Согласованность (Consistency)]]**: Если объекты не изменяются, многократный вызов `equals()` должен давать одинаковый результат.
- **[[Сравнение с null в контексте equals()]]**: Любой объект `x` при сравнении с `null` должен возвращать `false`.


При использовании метода `equals()`, необходимо учитывать ситуацию с `null`, при сравнение самих полей(**при использовании стандартной реализации** `equals()`).
Java метод `Objects.equals()` используется для удобного и безопасного сравнения объектов, особенно если один из них может быть `null`. Рассмотрим оба варианта сравнения и их различия.

#### 6. **В продолжении к `null` в контексте `equals()`:**
> [!WARNING] Важно учитывать, не безопасность метода `equals()` с `null`
> Вызов метода `equals()` на `null` приведет к возникновению исклбючения `NullPointerException`

| <span style="font-size: 1.04em; font-weight: bold; margin: 0; line-height: 1.2; display: inline-block; margin-bottom: 10px;"> Пример ошибки с `null`: </span>                                                                                                                                                                                                                                         |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Происходит **`NullPointerException`**, потому что метод `equals()` вызывается на `null`. [^1]                                                                                                                                                                                                                                                                                                         |
| <div class="code_md_tab"><br><code class="language-java language-java_td specific-override"><br>String str = null;<br></code><br><code class="language-java language-java_td specific-override"><br>System.out.println(str.equals("Hello")); // NullPointerException<br></code><br></div> Компактный и понятный метод, [[Objects.equals()]] корректно сравнивает значения, является лучшим вариантом. |

| <span style="font-size: 1.04em; font-weight: bold; margin: 0; line-height: 1.2; display: inline-block; margin-bottom: 10px;"> Решение №1<br>Проверка `null` перед вызовом `equals()`: </span><br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | <span style="font-size: 1.04em; font-weight: bold; margin: 0; line-height: 1.2; display: inline-block; margin-bottom: 10px;"> Решение №2<br>&nbsp;&nbsp; Сравнение `"Hello".equals(str)` (безопасный вызов на константе) </span>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| &nbsp;Можно явно(*в ручную*) проверить `null` перед вызовом метода: <div class="code_md_tab"><br><code class="language-java language-java_td specific-override"><br>public class Main {<br></code><br><code class="language-java language-java_td specific-override"><br>  public static void main(String[] args) {<br></code><br><code class="language-java language-java_td specific-override"><br>    String str = null;<br></code><br><code class="language-java language-java_td specific-override"><br>    System.out.println(str != null && str.equals("Hello")); // false, без ошибки<br></code><br><code class="language-java language-java_td specific-override"><br>  }<br></code><br><code class="language-java language-java_td specific-override"><br>}<br></code><br></div> Необходимо проверить **только объект на котором вызывается метод** `equals()`<br><br><div class="code_md_tab"><br><code class="language-java language-java_td specific-override"><br>public class Main {<br></code><br><code class="language-java language-java_td specific-override"><br>  public static void main(String[] args) {<br></code><br><code class="language-java language-java_td specific-override"><br>    String str = "";<br></code><br><code class="language-java language-java_td specific-override"><br>    System.out.println(str != null && str.equals(null)); // false, без ошибки<br></code><br><code class="language-java language-java_td specific-override"><br>  }<br></code><br><code class="language-java language-java_td specific-override"><br>}<br></code><br></div> **В аргументах метод допускает `null`**, в данном случае всегда выводится `false` <br>[[Сравнение с null в контексте equals()]]<br> | Вызов `equals()` на константе с установленным значением не `null`, **безопасен**.<br><div class="code_md_tab"><br><code class="language-java language-java_td specific-override"><br>public class Main {<br></code><br><code class="language-java language-java_td specific-override"><br>  public static void main(String[] args) {<br></code><br><code class="language-java language-java_td specific-override"><br>    String str = null;<br></code><br><code class="language-java language-java_td specific-override"><br>    System.out.println("Hello".equals(str)); // false, без ошибки<br></code><br><code class="language-java language-java_td specific-override"><br>  }<br></code><br><code class="language-java language-java_td specific-override"><br>}<br></code><br></div> В данном случае константа является строка `Hello`, так как строки не изменяемы. |

| <span style="font-size: 1.04em; font-weight: bold; margin: 0; line-height: 1.2; display: inline-block; margin-bottom: 10px;"> Решение №3  <br>   Использование `Objects.equals()` (==лучший вариант==) </span><br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Метод `Objects.equals()` предотвращает `NullPointerException`, так как он сам проверяет `null` перед сравнением:<br><div class="code_md_tab"><br><code class="language-java language-java_td specific-override"><br>import java.util.Objects;<br></code><br><code class="language-java language-java_td specific-override"><br> <br></code><br><code class="language-java language-java_td specific-override"><br>public class Main {<br></code><br><code class="language-java language-java_td specific-override"><br>  public static void main(String[] args) {<br></code><br><code class="language-java language-java_td specific-override"><br>   String str = null;<br></code><br><code class="language-java language-java_td specific-override"><br>   System.out.println(Objects.equals(str, "Hello")); // false, без ошибки<br></code><br><code class="language-java language-java_td specific-override"><br> }<br></code><br><code class="language-java language-java_td specific-override"><br>}<br></code><br></div> Компактный и понятный метод, [[Objects.equals()]] корректно сравнивает значения, является лучшим вариантом. |
*Еще пример с `null`:* [^2] 

#### 7. Разница `instanceof` и `getClass()` в `equals()`
Есть два способа проверять тип объекта в `equals()` ([[instanceof()]] и [[getClass()]]):

| <span style="font-size: 1.04em; font-weight: bold; margin: 0; line-height: 1.2; display: inline-block; margin-bottom: 10px;"> &nbsp;&nbsp; 🔹 С `instanceof` (учитывает наследование): </span><br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | <span style="font-size: 1.04em; font-weight: bold; margin: 0; line-height: 1.2; display: inline-block; margin-bottom: 10px;"> &nbsp;&nbsp; 🔹 С `getClass()` (строгое сравнение): </span>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <div class="code_md_tab"><br><code class="language-java language-java_td specific-override"><br>@Override<br></code><br><code class="language-java language-java_td specific-override"><br>public boolean equals(Object obj) {<br></code><br><code class="language-java language-java_td specific-override"><br>    if (this == obj) return true;<br></code><br><code class="language-java language-java_td specific-override"><br>    if (!(obj instanceof Person)) return false;<br></code><br><code class="language-java language-java_td specific-override"><br>    Person other = (Person) obj;<br></code><br><code class="language-java language-java_td specific-override"><br>    return name.equals(other.name);<br></code><br><code class="language-java language-java_td specific-override"><br>}<br></code>⠀⠀⠀⠀<br></div> | <div class="code_md_tab"><br><code class="language-java language-java_td specific-override"><br>@Override<br></code><br><code class="language-java language-java_td specific-override"><br>public boolean equals(Object obj) {<br></code><br><code class="language-java language-java_td specific-override"><br>    if (this == obj) return true;<br></code><br><code class="language-java language-java_td specific-override"><br>    if (obj == null \|\| this.getClass() != obj.getClass()) return false;<br></code><br><code class="language-java language-java_td specific-override"><br>    Person other = (Person) obj;<br></code><br><code class="language-java language-java_td specific-override"><br>    return name.equals(other.name);<br></code><br><code class="language-java language-java_td specific-override"><br>}<br></code>⠀⠀<br></div> |
| 📌 Позволяет `equals()` работать **корректно даже для подклассов**.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | 📌 Не позволит подклассу считаться равным суперклассу.<br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
#### 8. `equals()` и `hashCode()`
При переопределении `equals()` **обязательно** переопределять `hashCode()`.
*Пример:*
```java
@Override
public int hashCode() {
    return name.hashCode();
}
```
Это важно для корректной работы `HashMap`, `HashSet` и `HashTable`.

<table class="language-java_td" style="width: 99%; border-collapse: collapse; margin-bottom: 5px;">
	<tr>
		<strong style="font-size: 1.1em; color: #333;">Пример:</strong>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333; line-height: 1.7;"><span style="border: 1px solid black; padding: 2px;">#1</span>
		&nbsp; Пример <code>equals()</code> с разными полями:</strong> <!-- Заголовок первой колонки-->
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333; line-height: 1.7;"><span style="border: 1px solid black; padding: 2px;">#2</span>
		&nbsp; Пример <code>equals()</code> с разными полями (без ID):</strong>  <!-- Заголовок второй колонки-->
        </td>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre class="language-java_td" style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
class Employee {
    private String name;
    private int id;
 
    public Employee(String name, int id) {
        this.name = name;
        this.id = id;
    }
 
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (!(obj instanceof Employee)) return false;
        Employee other = (Employee) obj;
        return id == other.id && name.equals(other.name);
    }
 
    @Override
    public int hashCode() {
        return 31 * name.hashCode() + id;
    }
}
 
public class Main {
    public static void main(String[] args) {
        Employee e1 = new Employee("John", 101);
        Employee e2 = new Employee("John", 101);
        Employee e3 = new Employee("John", 102);
 
        System.out.println(e1.equals(e2)); // true
        System.out.println(e1.equals(e3)); // false (разные id)
    }
}
				</code>
            </pre>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
import java.util.Objects;
 
class Employee {
    private String name;
    private int age;
 
    public Employee(String name, int age) {
        this.name = name;
        this.age = age;
    }
 
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (!(obj instanceof Employee)) return false;
        Employee other = (Employee) obj;
        return age == other.age && Objects.equals(name, other.name);
    }
 
    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }
}
 
public class Main {
    public static void main(String[] args) {
        Employee e1 = new Employee("John", 30);
        Employee e2 = new Employee("John", 30);
        Employee e3 = new Employee("John", 35);
 
        System.out.println(e1.equals(e2)); // true (имя и возраст совпадают)
        System.out.println(e1.equals(e3)); // false (разный возраст)
    }
}
				</code>
            </pre>
        </td>
    </tr>
</table>

*[[hashCode()]]* - подробно

###### Подробнее <span style="border: 1px solid black; padding: 2px; line-height: 1.75;">#1</span>: &nbsp; <br/>
ID редко используется в `equals()`, если это уникальный идентификатор из базы данных. Однако в некоторых сценариях (например, если ID задается при создании объекта и не меняется) его можно учитывать.
###### Подробнее <span style="border: 1px solid black; padding: 2px; line-height: 1.75;">#2</span>: &nbsp; <br/>
📌 **Используем `Objects.equals(name, other.name)`, чтобы избежать `NullPointerException` при `null`.**
Такой подход позволяет корректно сравнивать объекты, когда ID **не является значимым полем** для `equals()`.

## 9. **Вывод**
1. **По умолчанию `equals()` сравнивает ссылки**. Нужно переопределять его для сравнения содержимого.
2. **Контракт `equals()` должен соблюдаться** (рефлексивность, симметричность, транзитивность, консистентность).
3. **Лучше использовать безопасный строгий `getClass()` с проверкой на `null`, но `instanceof` нужен если сравниваться могут и наследники в том числе**.
4. **Переопределяя `equals()`, всегда переопределяйте `hashCode()`**.
5. **Используйте `Objects.equals()` для безопасности при `null`**.
6. ** Так же лучше использовать `Objects.hash(name, age)`**.

<br/><div style="text-align: center; margin: 0; padding: 0;"> <span style="color: #ff7e5f; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> <span style="color: #feb47b; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> <span style="color: #4facfe; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> </div>

[^1]:**Что происходит?**  
	  - Переменная `str` содержит `null`, то есть она **не ссылается на объект**.  
	  - Метод `equals()` вызывается на `str`.  
	  - Так как `null` **не является объектом**, у него **нет методов**.  
	  - Попытка вызвать `.equals()` приводит к **исключению `NullPointerException`**.



[^2]:<table class="language-java_td" style="width: 99%; border-collapse: collapse; margin-bottom: 5px;">
		<tr>
			<strong style="font-size: 1.1em; color: #333;">Пример :</strong>
	    </tr>
	    <tr>
	        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
	            <strong style="font-size: 1em; color: #333; line-height: 1.5;"><span style="border: 1px solid black; padding: 2px;">#1</span>
	&nbsp; Сравнение без <code>Objects.equals()</code></strong><br/>
	Если вы используете стандартный метод <code>equals()</code>, необходимо учитывать ситуацию с <code>null</code> вручную:
	        </td>
	        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
	            <strong style="font-size: 1em; color: #333; line-height: 1.5;"><span style="border: 1px solid black; padding: 2px;">#2</span>
	&nbsp; Сравнение с <code>Objects.equals()</code><br/></strong>
	С <code>Objects.equals()</code> код становится проще и безопаснее:
	        </td>
	    </tr>
	    <tr>
	        <td style="padding: 5px 10px; border: 1px solid #ddd;">
	            <pre class="language-java_td" style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
					<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
	String str1 = null;
	 
	// Проверка вручную 
	if (str1 != null && str1.equals("Java")) {  🔴
	    System.out.println("Равны");
	} else {
	    System.out.println("Не равны");
	}
					</code>
	            </pre>
	        </td>
	        <td style="padding: 5px 10px; border: 1px solid #ddd;">
	            <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
					<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
	String str1 = null;
	String str2 = "Java";
	 
	if (Objects.equals(str1, str2)) {  🔴
	    System.out.println("Равны");
	} else {
	    System.out.println("Не равны");
	}
					</code>
	            </pre>
	        </td>
	    </tr>
	</table>
	
	###### Подробнее <span style="border: 1px solid black; padding: 2px; line-height: 1.75;">#1</span>: &nbsp; 🔴<br/>
	При использовании `equals()` на объекте `null` будет выброшено исключение:
	```java
	String str = null;
	System.out.println(str.equals("Hello")); // NullPointerException
	```
	но если `null` будет в аргументах сравнение пройдет корректно
	```java
	System.out.println("wew".equals(null));
	```
	###### Подробнее <span style="border: 1px solid black; padding: 2px; line-height: 1.75;">#2</span>: &nbsp; 🔴<br/>
	С `Objects.equals()` таких проблем нет:
	```java
	String str = null;
	System.out.println(Objects.equals(str, "Hello")); // false
	System.out.println(Objects.equals(null, null)); // true
	```
	`null` может быть в аргументах при этом исключение не выброситься даже если оба аргумента `null`

[^3]:🔹 **По умолчанию** метод `equals()` сравнивает ссылки, то есть два объекта равны, только если они указывают на одну область памяти.
	Пример:
	```java
	String s1 = new String("hello");
	String s2 = new String("hello");
	
	System.out.println(s1 == s2);       // false (разные объекты)
	System.out.println(s1.equals(s2));  // true (потому что String переопределяет equals)
	```

[^4]:## **Почему нужно переопределять `equals()`?**
	Если не переопределять `equals()`, сравнение будет происходить **по ссылке**, а не по содержимому. Это не всегда подходит, например, при сравнении объектов сущностей.
	
	*Пример без переопределения `equals()`:*
	```java
	class Person {
	    String name;
	
	    Person(String name) {
	        this.name = name;
	    }
	}
	
	public class Main {
	    public static void main(String[] args) {
	        Person p1 = new Person("Alice");
	        Person p2 = new Person("Alice");
	
	        System.out.println(p1.equals(p2)); // false (разные объекты)
	    }
	}
	```
	Здесь `p1` и `p2` с одинаковым именем, но `equals()` не переопределен, значит, сравниваются ссылки.
	## **Правильное переопределение `equals()`**
	Чтобы `equals()` работал правильно, он должен:
	1. **Соблюдать контракт `equals()`** (реализация должна быть **рефлексивной, симметричной, транзитивной, консистентной**).
	2. **Проверять `null`** (через `instanceof`, он сам обработает `null`).
	3. **Сравнивать только значимые поля**.
	4. **Переопределять `hashCode()`** при изменении `equals()`.
	### **Пример корректного `equals()`**
	```java
	class Person {
	    private String name;
	
	    public Person(String name) {
	        this.name = name;
	    }
	
	    @Override
	    public boolean equals(Object obj) {
	        if (this == obj) return true;  // Сравнение по ссылке
	        if (!(obj instanceof Person)) return false; // Проверка типа
	        Person other = (Person) obj; 
	        return name.equals(other.name); // Сравнение значимого поля
	    }
	
	    @Override
	    public int hashCode() {
	        return name.hashCode(); // Соответствие контракту equals() и hashCode()
	    }
	}
	
	public class Main {
	    public static void main(String[] args) {
	        Person p1 = new Person("Alice");
	        Person p2 = new Person("Alice");
	
	        System.out.println(p1.equals(p2)); // true (одинаковый name)
	    }
	}
	```
	📌 **Здесь `equals()` сравнивает содержимое, а не ссылки, что соответствует логике.**
	
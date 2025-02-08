**Рефлексивность означает, что объект должен быть равен самому себе.**
Чтобы проверить рефлексивность, можно вызывать`equals()` на одном и том же объекте. Так как по умолчанию метод [[boolean equals(Object obj)]] класса [[java.lang.Object]] имеет реализацию[^1]

- Для любого объекта `x`, вызов `x.equals(x)` всегда должен возвращать `true`.
- Это логично: ==**объект всегда равен самому себе**==.

```java
String str = "hello";
System.out.println(str.equals(str)); // true
```
Проверяется это следующей строкой:
```java
@Override
public boolean equals(Object obj) {
	if (this == obj) return true; // Рефлексивность
	...
}
```
`==` - **Проверяет равенство ссылок**
<br/><div style="text-align: center; margin: 0; padding: 0;"> <span style="color: #ff7e5f; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> <span style="color: #feb47b; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> <span style="color: #4facfe; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> </div>


[^1]:###### Пример cтандартной реализации в классе `Object`:
	```java
	public boolean equals(Object obj) {
	    return (this == obj); // Возвращает `true`, если оба объекта указывают на одну и ту же область памяти. 
	}
	```
	По умолчанию `equals()` проверяет равенство ссылок.
	###### Пример кастомного класса `Person`:
	```java
	public class Main {
	    public static void main(String[] args) {
	        Person p1 = new Person("Alice", 25);
	
	        // Проверка рефлексивности
	        System.out.println(p1.equals(p1)); // Должно быть true
	    }
	}
	```
	Чтобы метод `equals()` сравнивал содержимое объектов, а не ссылки он должен быть переопределен в классе `Person`. В нашем случае код и так выполнится корректно так как по умолчанию (**стандартная реализация метода `equals()` в классе `Object` проверяет равенство ссылок**, *пример выше*).
	
	Правильное переопределение метода `equals()` для класса `Person`:
	```java
	import java.util.Objects;
	
	class Person {
	    private String name;
	    private int age;
	
	    // Конструктор
	    public Person(String name, int age) {
	        this.name = name;
	        this.age = age;
	    }
	
	    // Переопределение метода equals()
	    @Override
	    public boolean equals(Object obj) {
	        if (this == obj) { // Проверка ссылки на идентичность (одна и та же ссылка)
	            return true;  
	        }
	        // Если объект `obj` равен `null` или его класс отличается от текущего, возвращаем `false`
	        if (obj == null || getClass() != obj.getClass()) {
	            return false;
	        }
	        Person person = (Person) obj; // Приведение к типу Person, чтобы получить доступ к его полям:
	        return age == person.age && Objects.equals(name, person.name); // Сравнение полей, Для сравнения строк используем метод `Objects.equals()`:
	    }
	
	    // Переопределение метода hashCode() для корректности
	    @Override
	    public int hashCode() {
	        return Objects.hash(name, age);
	    }
	}
	```
	
	о переопределить в классе код корректно выполнялся и возвращал `true` при вызове `p1.equals(p1)`, нужно убедиться, что метод `equals()` переопределен в классе `Person`. Если метод `equals()` не переопределен, он наследуется от класса `Object`, где по умолчанию сравниваются ссылки, а не содержимое объектов.
	
	
	
	Чтобы этот код корректно выполнялся и возвращал `true` при вызове `p1.equals(p1)`, нужно убедиться, что метод `equals()` переопределен в классе `Person`. Если метод `equals()` не переопределен, он наследуется от класса `Object`, где по умолчанию сравниваются ссылки, а не содержимое объектов.
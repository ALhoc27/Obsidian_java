Транзитивность — это одно из ключевых свойств метода `equals()` в Java, указанное в контракте метода `equals()` (из класса `Object`).

> [!NOTE] Правило
> Согласно **контракту `equals()`**, если объект `A` равен объекту `B`, а объект `B` равен объекту `C`, то объект `A` должен быть равен объекту `C`.<br/>
> **Иными словами:** 
> &nbsp;&nbsp; Если  `a.equals(b) == true` и `b.equals(c) == true` равны, то `a.equals(c)` так же должен быть равен `true`

***Пример нарушения транзитивности:*** [^1]
```java
@Override
public boolean equals(Object obj) {
	if (this == obj) return true;

	if (obj instanceof Person) {
		Person other = (Person) obj;

		// Условие для демонстрации нарушения транзитивности:
		// Если одно из имен — "Admin", то считаем объекты равными.
		if ("Admin".equals(this.name) || "Admin".equals(other.name)) {
			return true;
		}

		// В других случаях сравниваем по имени.
		return this.name.equals(other.name);
	}

	return false;
}

...
Person p1 = new Person("Alice");
Person p2 = new Person("Admin");
Person p3 = new Person("Bob");

// Проверяем транзитивность:
System.out.println("p1_p2" + new Person("Alice").equals(new Person("Admin"))); // true, из-за условия "Admin"
System.out.println("p2_p3" + new Person("Admin").equals(new Person("Bob")));   // true, из-за условия "Admin"
System.out.println("p1_p3" + new Person("Alice").equals(new Person("Bob")));   // false, так как "Alice" != "Bob"
    }
```
##### **Что здесь происходит?**
Метод `equals()` использует разную логику для разных объектов:
- Для имени "Admin" используется упрощённая логика, где объект автоматически считается равным любому другому.
- Для остальных объектов сравнение идёт строго по значению `name`.

**Нарушение транзитивности**:  
Если `"p1_p2"` и `"p2_p3"` оба вернули `true`, то транзитивность требует, чтобы `"p1_p3"` тоже вернуло `true`. Но в данном случае это не так.

#### **Как исправить?**
Для исправления нужно использовать **одинаковую логику сравнения для всех объектов**. Например, убрать исключение для имени "Admin".
```java
@Override
public boolean equals(Object obj) {
    if (this == obj) return true;

    if (obj instanceof Person) {
        Person other = (Person) obj;
        return this.name.equals(other.name); // Строгое сравнение только по имени
    }

    return false;
}
```

### **Заключение**
1. Транзитивность можно соблюдать, если:
    - Логика `equals()` является консистентной^[В контексте метода `equals()` в Java **консистентность** означает, что результат вызова метода `equals()` для одних и тех же объектов не изменится, если состояние этих объектов остаётся неизменным.] и основывается на сравнимых данных.
    - Методы для суперклассов и подклассов правильно используют `super.equals()`.
2. Для этого важно тестировать объекты, чтобы убедиться, что они соответствуют всем требованиям контракта `equals()`.
3. Нарушение транзитивности может привести к непредсказуемым результатам, например, в коллекциях (`HashSet`, `HashMap`), где поведение зависит от `equals()` и `hashCode()`.


<br/><div style="text-align: center; margin: 0; padding: 0;"> <span style="color: #ff7e5f; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> <span style="color: #feb47b; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> <span style="color: #4facfe; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> </div>

[^1]:```java
	class Person {
	    private String name;
	
	    public Person(String name) {
	        this.name = name;
	    }
	
	    @Override
	    public boolean equals(Object obj) {
	        if (this == obj) return true;
	
	        if (obj instanceof Person) {
	            Person other = (Person) obj;
	
	            // Условие для демонстрации нарушения транзитивности:
	            // Если одно из имен — "Admin", то считаем объекты равными.
	            if ("Admin".equals(this.name) || "Admin".equals(other.name)) {
	                return true;
	            }
	
	            // В других случаях сравниваем по имени.
	            return this.name.equals(other.name);
	        }
	
	        return false;
	    }
	
	    @Override
	    public int hashCode() {
	        return name.hashCode();
	    }
	}
	
	public class Main {
	    public static void main(String[] args) {
	        Person p1 = new Person("Alice");
	        Person p2 = new Person("Admin");
	        Person p3 = new Person("Bob");
	
	        // Проверяем транзитивность:
	        System.out.println("p1.equals(p2): " + p1.equals(p2)); // true, из-за условия "Admin"
	        System.out.println("p2.equals(p3): " + p2.equals(p3)); // true, из-за условия "Admin"
	        System.out.println("p1.equals(p3): " + p1.equals(p3)); // false, так как "Alice" != "Bob"
	    }
	}
	```
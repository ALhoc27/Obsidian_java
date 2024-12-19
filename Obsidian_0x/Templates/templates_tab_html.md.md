<table class="language-java_td" style="width: 99%; border-collapse: collapse; margin-bottom: 5px;">
	<tr>
		<strong style="font-size: 1.1em; color: #333;">Пример 1:</strong>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333;"><span style="border: 1px solid black; padding: 2px;">#1</span>
&nbsp; У нас есть класс `Person`, где мы хотим сравнивать людей по имени:</strong>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333;"><span style="border: 1px solid black; padding: 2px;">#2</span>
&nbsp; У нас есть класс `Student`, где мы хотим сравнивать людей по возврасту:</strong>
        </td>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre class="language-java_td" style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
import java.util.Arrays;  
 
public class Person implements Comparable＜Person＞ {  
	String name;  
	 
	public Person(String name) {  
		this.name = name;  
	}  
	 
	@Override  
	public String toString() {  
		return '{' + name + '}';  
	}  
	  
	@Override  
🔴  public int compareTo(Person o) {  // Выполняется сравнение строковых полей `name` двух объектов `Person`
	 return this.name.compareTo(o.name);  
	}  
   
}  
  
class Main {  
	public static void main(String[] args) {  
		Person[] names = {new Person("Alice"), new Person("Charlie"), new Person("Bob")};  
		Arrays.sort(names); // Вызовет compareTo у String  
		System.out.println(Arrays.toString(names));  
	}  
}
				</code>
            </pre>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
import java.util.ArrayList;  
import java.util.Collections;  
 
public class Student implements Comparable＜Student＞ {  
	private int age;  
	  
	public Student(int age) {  
		this.age = age;  
	}  
	  
	@Override  
	public String toString() {  
		return "{" + age + "}";  
	}  
	  
	@Override  
	public int compareTo(Student other) {  
		return this.age - other.age; // Сортировка по возрасту  
	}  
}  
  
class Main {  
	public static void main(String[] args) {  
		ArrayList＜Student＞ people = new ArrayList＜＞();  
		people.add(new Student(12));  
		people.add(new Student(23));  
		people.add(new Student(43));  
	 	
		Collections.sort(people); // Используется compareTo()  
		System.out.println(people); // Вывод: [Alice, Bob, Charlie]  
	}  
}
				</code>
            </pre>
        </td>
    </tr>
</table>

###### Подробнее <span style="border: 1px solid black; padding: 2px; line-height: 1.75;">#1</span>:<br/>
 &nbsp;🔴 - Метод `compareTo` для строк сравнивает их лексикографически (помещая строку "меньше", если она идет раньше в алфавите).
 &nbsp;🟠 -
 &nbsp;🟤 -
 &nbsp;🟣 -
 &nbsp;🔵 -
 &nbsp;🟡 -
 &nbsp;🟢 -
 &nbsp;⚪️ -
 &nbsp;⚫️ -

###### Подробнее <span style="border: 1px solid black; padding: 2px; line-height: 1.75;">#2</span>:<br/>
 &nbsp;🔴 - Метод `compareTo` для строк сравнивает их лексикографически (помещая строку "меньше", если она идет раньше в алфавите).
 &nbsp;🟠 -
 &nbsp;🟤 -
 &nbsp;🟣 -
 &nbsp;🔵 -
 &nbsp;🟡 -
 &nbsp;🟢 -
 &nbsp;⚪️ -
 &nbsp;⚫️ -



> - **Замени все <> на ＜＞**
> - **Поставь в коде пробелы где пустая строка**
> - 🔴 **шарик 2 пробела**
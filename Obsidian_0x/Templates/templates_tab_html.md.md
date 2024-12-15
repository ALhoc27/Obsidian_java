<table style="width: 100%; border-collapse: collapse; margin-bottom: 20px;">
    <tr>
        <td style="padding: 10px; border: 1px solid #ddd;">
            <strong style="font-size: 1.1em; color: #333;">Создание экземпляра с помощью конструктора</strong>
        </td>
        <td style="padding: 10px; border: 1px solid #ddd;">
            <strong style="font-size: 1.1em; color: #333;">Использование конструктора через рефлексию</strong>
        </td>
    </tr>
    <tr>
        <td style="padding: 10px; border: 1px solid #ddd;">
            <pre style="background-color: #f4f4f4; color: #f8f8f8; padding: 15px; border-radius: 5px; font-size: 0.9em; overflow-x: auto; white-space: pre-wrap;">
<code class="language-java" style="font-family: 'Courier New', monospace;">
class Person {
    String name;
    int age;
 
    // Конструктор с параметрами
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
 
public class Main {
    public static void main(String[] args) {
        // Создание экземпляра с помощью конструктора с параметрами
        Person person = new Person("Alice", 30);
        System.out.println(person.name + " - " + person.age); // Alice - 30
    }
}
</code>
            </pre>
        </td>
        <td style="padding: 10px; border: 1px solid #ddd;">
            <pre style="background-color: #f4f4f4; color: #f8f8f8; padding: 15px; border-radius: 5px; font-size: 0.9em; overflow-x: auto; white-space: pre-wrap;">
<code class="language-java" style="font-family: 'Courier New', monospace;">
import java.lang.reflect.Constructor;
 
  
public class Main {
    public static void main(String[] args) {
        try {
            // Получаем объект Class для Person
            Class<?> clazz = Person.class;
   
            // Получаем конструктор с параметрами
            Constructor<?> constructor = clazz.getConstructor(String.class, int.class);
  
            // Создаем новый экземпляр
            Person person = (Person) constructor.newInstance("Bob", 25);
            System.out.println(person.name + " - " + person.age); // Bob - 25
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
</code>
            </pre>
        </td>
    </tr>
    <tr>
        <td style="padding: 10px; border: 1px solid #ddd;">
            <strong style="font-size: 1.1em; color: #333;">Вывод:</strong><br>
            Alice - 30
        </td>
        <td style="padding: 10px; border: 1px solid #ddd;">
            <strong style="font-size: 1.1em; color: #333;">Вывод:</strong><br>
            Bob - 25
        </td>
    </tr>
</table>
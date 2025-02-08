Метод `fieldModifiers()` из класса `java.lang.reflect.Modifier` возвращает целое число, представляющее битовую маску, содержащую все возможные модификаторы, которые могут быть применены к полям (переменным) в Java.
#### Сигнатура
```java
public static int fieldModifiers()
```
- **Возвращаемое значение**: целое число (тип `int`), представляющее битовую маску всех допустимых модификаторов для полей.
#### Модификаторы полей
Поля в Java могут иметь следующие модификаторы:
1. **`public`** – поле доступно везде.
2. **`protected`** – поле доступно внутри пакета и подклассам вне пакета.
3. **`private`** – поле доступно только внутри того же класса.
4. **`static`** – поле принадлежит классу, а не экземпляру класса.
5. **`final`** – значение поля не может быть изменено после инициализации.
6. **`transient`** – поле не сохраняется при сериализации.
7. **`volatile`** – гарантирует, что каждый поток будет видеть последние изменения значения поля.

<table class="language-java_td" style="width: 99%; border-collapse: collapse; margin-bottom: 5px;">
	<tr>
		<strong style="font-size: 1.1em; color: #333;">Пример использования:</strong>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333;"><span style="border: 1px solid black; padding: 2px;">#1</span>
&nbsp; Пример 1: Получение всех допустимых модификаторов для полей:</strong>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333;"><span style="border: 1px solid black; padding: 2px;">#2</span>
&nbsp; Пример 2: Проверка модификаторов конкретного поля:</strong>
        </td>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre class="language-java_td" style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
import java.lang.reflect.Modifier;
 
public class Main {
    public static void main(String[] args) {
        // Получаем допустимые модификаторы для полей
        int modifiers = Modifier.fieldModifiers();
 
        // Преобразуем модификаторы в строку
        String modifiersString = Modifier.toString(modifiers);
 
        System.out.println("Допустимые модификаторы для полей: " + modifiersString);
    }
}
				</code>
            </pre>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
import java.lang.reflect.Field;
import java.lang.reflect.Modifier;
 
class Example {
    public static final int CONSTANT = 42;
    private transient String name;
}
 
public class Main {
    public static void main(String[] args) throws Exception {
        // Получаем поле "CONSTANT"
        Field constantField = Example.class.getField("CONSTANT");
        int constantModifiers = constantField.getModifiers();
 
        System.out.println("CONSTANT модификаторы: " + Modifier.toString(constantModifiers));
        System.out.println("Is static? " + Modifier.isStatic(constantModifiers));  // true
        System.out.println("Is final? " + Modifier.isFinal(constantModifiers));    // true
 
        // Получаем поле "name"
        Field nameField = Example.class.getDeclaredField("name");
        int nameModifiers = nameField.getModifiers();
 
        System.out.println("\nname модификаторы: " + Modifier.toString(nameModifiers));
        System.out.println("Is private? " + Modifier.isPrivate(nameModifiers));     // true
        System.out.println("Is transient? " + Modifier.isTransient(nameModifiers)); // true
    }
}
				</code>
            </pre>
        </td>
    </tr>
</table>

###### Подробнее <span style="border: 1px solid black; padding: 2px; line-height: 1.75;">#1</span>: &nbsp; <br/>
Вывод:
```java
Допустимые модификаторы для полей: public protected private static final transient volatile
```

###### Подробнее <span style="border: 1px solid black; padding: 2px; line-height: 1.75;">#2</span>: &nbsp; <br/>
Вывод:
```java
CONSTANT модификаторы: public static final
Is static? true
Is final? true

name модификаторы: private transient
Is private? true
Is transient? true
```

#### Реальный пример анализа полей с модификаторами (кастомный класс)
```java
import java.lang.reflect.Field;
import java.lang.reflect.Modifier;

class Person {
    public String name;
    private int age;
    protected static final String SPECIES = "Homo sapiens";
    transient int tempData;
}

public class Main {
    public static void main(String[] args) {
        // Получаем все поля класса Person
🟠      Field[] fields = Person.class.getDeclaredFields();

        System.out.println("Анализ полей класса Person:");
🟤      for (Field field : fields) {
            // Имя поля
            String fieldName = field.getName();
            // Модификаторы поля
            int modifiers = field.getModifiers();
            String modifiersString = Modifier.toString(modifiers);

            System.out.printf("Поле: %s, Модификаторы: %s%n", fieldName, modifiersString);
        }
    }
}
```
**Вывод:**
```yaml
Анализ полей класса Person:
Поле: name, Модификаторы: public
Поле: age, Модификаторы: private
Поле: SPECIES, Модификаторы: protected static final
Поле: tempData, Модификаторы: transient
```

🟠 
```java
Field[] fields = Person.class.getDeclaredFields();
```
- `Person.class`: возвращает объект `Class`, представляющий класс `Person`.
- `getDeclaredFields()`: возвращает массив объектов `Field`, представляющих все поля класса `Person`, включая `private`, `protected`, и `transient`. Наследованные поля не учитываются.

🟤
```java
for (Field field : fields) {
    // Имя поля
    String fieldName = field.getName();
    // Модификаторы поля
    int modifiers = field.getModifiers();
    String modifiersString = Modifier.toString(modifiers);

    System.out.printf("Поле: %s, Модификаторы: %s%n", fieldName, modifiersString);
}
```
- `field.getName()`: возвращает имя текущего поля (например, `"name"`).
- `field.getModifiers()`: возвращает модификаторы поля в виде числа (битовая маска).
- `Modifier.toString(modifiers)`: преобразует модификаторы в удобный строковый вид.
<b>"Поле: %s, Модификаторы: %s%n" - подробнее</b> [^4]

<br/><div style="text-align: center; margin: 0; padding: 0;"> <span style="color: #ff7e5f; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> <span style="color: #feb47b; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> <span style="color: #4facfe; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> </div>

[^4]:![[Снимок экрана 2025-01-12 в 23.12.18.png|500]]
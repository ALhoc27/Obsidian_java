#### Как заполнять `Code with comments`
1. Создаете папку с проектом (то же название)
2. Переносите весь проект по файлам (все что java, все что будем разбирать) в эту папку (всю структуру)
	1. Код проекта должен быть на **github**
3. Для каждого файла, требуется создать дубликат с приставкой в конце 0x
   ![[Снимок экрана 2024-12-04 в 17.47.48.png|200]]
   В данном файле полностью описывается код оригинального
   **==(НО ВСЕ КЛАССЫ И МЕТОДЫ ДОЛЖНЫ БЫТЬ ЗАНЕСЕНЫ В БАЗУ, ТУТ СОДЕРЖАТСЯ ТОЛЬКО ССЫЛКИ)==**
4. База знаний содержится в папке `Class && Interface`
   ![[Снимок экрана 2024-12-04 в 17.48.12.png|200]]
Все классы, методы, интерфейсы находятся именно тут.

##### Ссылки
<pre>[Obsidian](http://obsidian.md)</pre>

#### Format

Пример простой сноски[^1] 
Пример сноски прямо в коде^[Сноска]

В Obsidian есть несколько встроенных типов блоков, которые можно использовать для выделения информации в заметках. Вот основные типы:

1. **[!NOTE]** – для обычных заметок.    !NOTE
2. **[!TIP]** – для полезных советов.    !TIP
3. **[!INFO]** – для предоставления дополнительной информации.    !INFO
4. **[!WARNING]** – для предупреждений.    !WARNING
5. **[!DANGER]** – для обозначения опасных действий или серьезных предупреждений.    !DANGER

| ![[Снимок экрана 2024-12-04 в 19.17.33.png\|300]] | 200 - размер изображения |
| ------------------------------------------------- | ------------------------ |
<details> 
<summary>Объектно-Ориентированное Программирование</summary> 
Не поддерживается форматирование внутри блока, только текст
</details>



|                                                                                                                                                                                                                                                              |                                                                                                                                                                                                                                                                                          |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Работа с одним типом данных:**<br>    <br>    - `switch` удобен для проверки значений типов `int`, `byte`, `short`, `char`, `String`, `enum`.<br>    - С новыми версиями Java поддерживаются строки и перечисления (`enum`), что делает его универсальным. | **Не фиксированные значения:**<br>    <br>    - Когда значения, с которыми сравнивается переменная, не фиксированы (например, вычисляются в процессе), `if-else` становится единственным вариантом.<br>- **Логические комбинации                                                         |
| <pre class="jcode"><br>public class HelloWorld {<br>    public static void main(String[] args) {<br>        System.out.println("Hello, World!");<br>    }<br>}<br></pre>                                                                                     | <pre class="jcode"><br>int day = 3;<br>    <br>switch (day) {<br>    case 1 -> System.out.println("Понедельник");<br>    case 2 -> System.out.println("Вторник");<br>    case 3 -> System.out.println("Среда");<br>    default -> System.out.println("Неизвестный день");<br>}<br></pre> |
| Какой то текст                                                                                                                                                                                                                                               | Какой то текст                                                                                                                                                                                                                                                                           |
|                                                                                                                                                                                                                                                              |                                                                                                                                                                                                                                                                                          |

<br>

#### Для того что бы в таблице отображался код:
<table>
	<tr>
		<td> 
			<strong>
		Пример 1
			</strong>
		</td>
		<td> 
			<strong>
		Пример 2
			</strong>
		</td> 
	</tr>
	<tr>
		<td>
			<pre>
				<code class="language-java">
int day = 1;
 
switch (day) {
	case 1:
		System.out.println("Понедельник");
	case 2:
		System.out.println("Вторник");
	case 3:
		System.out.println("Среда");
		break;
	default:
		System.out.println("Некорректный день");
}
				 </code>
			 </pre>
		 </td>
		 <td>
			<pre>
				<code class="language-java">
int day = 2;
 
switch (day) {
	case 1:
		System.out.println("Понедельник");
	case 2:
		System.out.println("Вторник");
	case 3:
		System.out.println("Среда");
		break;
	default:
		System.out.println("Некорректный день");
}
				 </code>
			 </pre>
		 </td>
	 </tr>
	  <tr>
		<td> 
			<strong>
				Вывод: 
			</strong>
				...
		</td>
		<td> 
			<strong>
				Вывод: 
			</strong>
				... <br>
				...
		</td> 
	</tr>
 </table>


####  либо такой стиль (не забывайте ставить пробелы в коде где имеется перевод строки):

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

В случае когда синтаксис в таблице в коде с отсутпом в строку отображается некорректно**==(то для корректного отображения кода БЕЗ РАЗДЕЛЕНИЯ необходимо в пробельной строке поставить пару пробелов==**)
** Так же может сбится просмотр кода, для этого внесите всю таблицу в код  `   ````   ````   ` ** (за комментируйте пока пишите лекцию)


> **Такой вариант подойдет если описание требуется немного каждого столбца**
> Но если требуется таблица с кодом и описанием как ниже (используйте тек `pre` с классом `class="jcode"`)

> [!NOTE]
> 

> [!TIP]
> 

> [!INFO]
> 

> [!WARNING]

> [!DANGER]


Добавляет визуальные акценты для привлечения внимания:

- ✅ Пример: Этот метод работает корректно.
- ⚠️ Пример: Обратите внимание на возможные ошибки.
- ❗️ Пример: Внимание
- ❌ Пример: Не используйте этот подход.

#### Подсветка синтаксиса (yaml)
``` yaml
Имя класса: java.lang.String
```

 🔎 Рефлексия 🔍


https://publish.obsidian.md/help-ru/Руководства/Форматирование+заметок
https://docs.oracle.com/en/java/javase/23/docs/api/index.html





[^1]:
	Сноска

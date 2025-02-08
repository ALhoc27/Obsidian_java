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

<table style="
    width: 100%; 
    border-collapse: collapse; 
    font-family: Arial, sans-serif; 
    font-size: 16px; 
    text-align: left; 
    margin: 20px 0; 
    background: linear-gradient(120deg, #f3f4f6, #e9ecef); 
    border-radius: 8px; 
    overflow: hidden; 
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    .code
">
    <thead>
        <tr>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td style="padding: 12px 15px; border-bottom: 1px solid #d6d8db;" class="styled-table"> - Если <code>A</code> имеет метод <code>foo()</code>, то <code>D</code> наследует этот метод дважды — один раз через <code>B</code> и ещё раз через <code>C</code>. <br>&nbsp;- JVM не может определить, какую версию <code>foo()</code> использовать: из <code>B</code> или из <code>C</code>.</td>
        </tr>
    </tbody>
</table>
<dir style="
    width: 100%; 
    border-collapse: collapse; 
    font-family: Arial, sans-serif; 
    font-size: 13px; 
    text-align: left; 
    margin: 20px 5px; 
    padding: 5px 5px; 
    background-color: rgba(255, 165, 0, 0.3);
    border-radius: 8px; 
    overflow: hidden; 
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
	border: 1px solid #d6d8db;
">
    <span class="styled-table"> - Если <code>A</code> имеет метод <code>foo()</code>, то <code>D</code> наследует этот метод дважды — один раз через <code>B</code> и ещё раз через <code>C</code>. <br>&nbsp;- JVM не может определить, какую версию <code>foo()</code> использовать: из <code>B</code> или из <code>C</code>.</span>
    <br>
</dir>

<span style="background-color: rgba(255, 165, 0, 0.3); font-weight: normal; padding: 2px 6px; border: 1px solid #ccc;"> - Если `A` имеет метод `foo()`, то `D` наследует этот метод дважды — один раз через `B` и ещё раз через `C`. <br> &nbsp; - JVM не может определить, какую версию `foo()` использовать: из `B` или из `C`.
</span>

<table style="
    width: 100%; 
    border-collapse: collapse; 
    font-family: Arial, sans-serif; 
    font-size: 16px; 
    text-align: left; 
    margin: 20px 0; 
    background: linear-gradient(120deg, #f3f4f6, #e9ecef); 
    border-radius: 8px; 
    overflow: hidden; 
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
">
    <thead>
        <tr>
            <th style="background-color: #6c757d; color: white; padding: 12px 15px;">#</th>
            <th style="background-color: #6c757d; color: white; padding: 12px 15px;">Название</th>
            <th style="background-color: #6c757d; color: white; padding: 12px 15px;">Описание</th>
            <th style="background-color: #6c757d; color: white; padding: 12px 15px;">Дата</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td style="padding: 12px 15px; border-bottom: 1px solid #d6d8db;">1</td>
            <td style="padding: 12px 15px; border-bottom: 1px solid #d6d8db;">Заголовок</td>
            <td style="padding: 12px 15px; border-bottom: 1px solid #d6d8db;">Пример описания</td>
            <td style="padding: 12px 15px; border-bottom: 1px solid #d6d8db;">2024-12-17</td>
        </tr>
    </tbody>
</table>

---

<dir style="
    width: 100%; 
    border-collapse: collapse; 
    font-family: Arial, sans-serif; 
    font-size: 13px; 
    text-align: left; 
    margin: 20px 5px; 
    padding: 5px 5px; 
    background-color: rgba(255, 165, 0, 0.3);
    border-radius: 8px; 
    overflow: hidden; 
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
	border: 1px solid #d6d8db;
">
<strong>&nbsp;- Путь для java лекций:</strong> <code>path:"Obsidian_Java/Java/Learn Java/Учебный материал"</code><br><strong>&nbsp;- Class && Interface:</strong> &nbsp; &nbsp; &nbsp; <code>path:"Obsidian_Java/Java/Сlass && Interface"</code></dir>

| <span style="white-space: nowrap; line-height: 1.8; border: 1px solid black; padding: 2px;"><strong> [[JAVA CORE]] </strong> </span> <span style="white-space: nowrap; line-height: 1.8; background-color: rgba(255, 165, 0, 0.3); font-weight: normal; padding: 2px 6px; border: 1px solid #ccc;"> <strong> [[Сlass && Interface]] </strong> </span> <span style="white-space: nowrap; line-height: 1.8; background-color: rgba(255, 165, 0, 0.3); font-weight: normal; padding: 2px 6px; border: 1px solid #ccc;"> <strong> [[Java (Test)]] </strong> </span> <span style="white-space: nowrap; line-height: 1.8; background-color: rgba(255, 165, 0, 0.3); font-weight: normal; padding: 2px 6px; border: 1px solid #ccc;"> <strong> [[Java (Паттерны)]] </strong> </span> | ![[Снимок экрана 2024-12-18 в 22.57.45.png\|700]] [^1] |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ |

<table style="
    width: 100%; 
    border-collapse: collapse; 
    font-family: Arial, sans-serif; 
    font-size: 16px; 
    text-align: left; 
    margin: 20px 0; 
    background: linear-gradient(120deg, #f3f4f6, #e9ecef); 
    border-radius: 8px; 
    overflow: hidden; 
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
">
    <thead>
        <tr>
            <th style="background-color: #6c757d; color: white; padding: 12px 15px;">Поиск:</th>
            <th style="background-color: #6c757d; color: white; padding: 12px 15px;">в Obsidian (глобальный поиск)</th>
            <th style="background-color: #6c757d; color: white; padding: 12px 15px;">в Obsidian (быстрый поиск)</th>
            <th style="background-color: #6c757d; color: white; padding: 12px 15px;">в Omnisearch</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td style="padding: 12px 15px; border-bottom: 1px solid #d6d8db;">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;<a href="obsidian://open?vault=Obsidian_Java&file=Obsidian_Java%2FJava%2FOther%20tools%2FOther%2F%D0%9F%D0%BE%D0%B4%D1%80%D0%BE%D0%B1%D0%BD%D0%B5%D0%B5%20%D0%BF%D0%BE%D0%B8%D1%81%D0%BA%20Omnisearch">Info</a></td>
            <td style="padding: 12px 15px; border-bottom: 1px solid #d6d8db;">Открывает глобальный поиск по всем заметкам в вашем хранилище (vault)
<span style="border: 1px solid black; padding: 2px;"><code>Shift + Command + F</code></span><br/></td>
            <td style="padding: 12px 15px; border-bottom: 1px solid #d6d8db;">Открывает быстрый поиск и переключение между заметками.
<span style="border: 1px solid black; padding: 2px;"><code>Command + O</code></span><br/></td>
            <td style="padding: 12px 15px; border-bottom: 1px solid #d6d8db;">Поиск с помощью расширения Omnisearch (<a href="obsidian://open?vault=Obsidian_Java&file=Obsidian_Java%2FJava%2FOther%20tools%2FOther%2F%D0%9F%D0%BE%D0%B4%D1%80%D0%BE%D0%B1%D0%BD%D0%B5%D0%B5%20%D0%BF%D0%BE%D0%B8%D1%81%D0%BA%20Omnisearch">Подробнее</a>)
<span style="border: 1px solid black; padding: 2px;"><code>Command + Shift + O</code></span><br/></td>
        </tr>
    </tbody>
</table>
<table style="
    width: 100%; 
    border-collapse: collapse; 
    font-family: Arial, sans-serif; 
    font-size: 16px; 
    text-align: left; 
    margin: 0px; 
    padding: 0px;
    background: linear-gradient(120deg, #f3f4f6, #e9ecef); 
    border-radius: 8px; 
    overflow: hidden; 
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
">
    <thead>
        <tr>
            <th style="background-color: #6c757d; color: white; padding: 12px 15px;">Поиск:</th>
            <th style="background-color: #6c757d; color: white; padding: 12px 15px;">в Obsidian (глобальный поиск)</th>
            <th style="background-color: #6c757d; color: white; padding: 12px 15px;">в Obsidian (быстрый поиск)</th>
            <th style="background-color: #6c757d; color: white; padding: 12px 15px;">в Omnisearch</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td style="padding: 12px 15px; border-bottom: 1px solid #d6d8db;"><strong><a href="obsidian://open?vault=Obsidian_Java&file=Obsidian_Java%2FObsidian_0x%2FFind%20(info)">Find (info)</a></strong></td>
            <td style="padding: 0px 0px 12px 10px; border-bottom: 1px solid #d6d8db;">
<span style="border: 1px solid black; padding: 2px;"><code>Shift + Command + F</code></span><br/></td>
            <td style="padding: 0px 0px 12px 10px; border-bottom: 1px solid #d6d8db;">
<span style="border: 1px solid black; padding: 2px;"><code>Command + O</code></span><br/></td>
            <td style="padding: 0px 0px 12px 10px; border-bottom: 1px solid #d6d8db;">
<span style="border: 1px solid black; padding: 2px;"><code>Command + Shift + O</code></span><br/></td>
        </tr>
    </tbody>
</table>

| Поиск: | в Obsidian (глобальный поиск)                                                                | в Obsidian (быстрый поиск)                                                           |                                         в Omnisearch                                         |
| ------ | -------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------: |
|        | <span style="border: 1px solid black; padding: 2px;"><code>Shift + Command + F</code></span> | <span style="border: 1px solid black; padding: 2px;"><code>Command + O</code></span> | <span style="border: 1px solid black; padding: 2px;"><code>Command + Shift + O</code></span> |


<dir style="background-color: transparent; color: #333; padding: 3px 6px; border-radius: 3px; font-size: 15px; font-family: -apple-system, BlinkMacSystemFont, Roboto, Helvetica Neue, Arial, sans-serif;">Исключения ( <span style="background-color: #f4f4f4; padding: 4px; border-radius: 3px; overflow: auto; font-family: 'Courier New', Courier, monospace;">Exceptions</span> ) позволяют программисту корректно реагировать на ошибки, предотвращая крах приложения.</dir>


<table class="language-java_td" style="width: 99%; border-collapse: collapse; margin-bottom: 5px;">
	<tr>
		<strong style="font-size: 1.1em; color: #333;">Пример:</strong>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333;"><span style="border: 1px solid black; padding: 2px;">#1</span>
&nbsp; У нас есть класс `Person`, где мы хотим сравнивать людей по имени:</strong>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333;"><span style="border: 1px solid black; padding: 2px;">#2</span>
&nbsp; У нас есть класс `Person`, где мы хотим сравнивать людей по имени:</strong>
        </td>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto; white-space: pre-wrap;">
<code class="language-java" style="font-family: 'Courier New', monospace;">
class Person implements Comparable<Person> {
    private String name;
     
    // Конструктор и геттеры/сеттеры опущены для краткости...
 
    @Override
    public int compareTo(Person other) {
        return this.name.compareTo(other.getName());
    }
}
</code>
            </pre>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto; white-space: pre-wrap;">
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
        <td style="padding: 5px 10px; border: 1px solid #ddd; font-size: 0.9em;">
            <strong style="font-size: 1em; color: #333;">Вывод:</strong><br>
            Alice - 30
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd; font-size: 0.9em;">
            <strong style="font-size: 1em; color: #333;">Вывод:</strong><br>
            Bob - 25
        </td>
    </tr>
</table>

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
            <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
<code class="language-java" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
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
🟠      return this.name.compareTo(o.name);  
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
<code class="language-java" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
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
        ArrayList＜Student＞ people = new ArrayList<>();  
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
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd; font-size: 0.9em;">
            <strong style="font-size: 1em; color: #333;">Вывод:</strong><br>
<pre style="background-color: #f4f4f4; color: #696969; margin: 5px; padding: 10px 0px 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
[{Alice}, {Bob}, {Charlie}]
 
Process finished with exit code 0
            </pre>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd; font-size: 0.9em;">
            <strong style="font-size: 1em; color: #333;">Ключевой момент:</strong>
		<pre class="jcode">
@Override  
public int compareTo(Student other) {  
	return this.age - other.age; // Сортировка по возрасту  
}  
		</pre>
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




> ***Например:***
> 1. **Сортировке** (`Arrays.sort`, `Collections.sort`, `Stream.sorted()`)
> 	- `Arrays.sort`:
> 	```java
> 	Arrays.sort(array); // Сортирует массив объектов, реализующих Comparable
> 	```
> 	- `Collections.sort`:
> 	```java
> 	List<String> list = Arrays.asList("Charlie", "Alice", "Bob");
> 	Collections.sort(list); // Сортирует список
> 	```
> 	- `Stream.sorted()`:
> 	```java
> 	list.stream().sorted().forEach(System.out::println); // Потоковая сортировка
> 	```
> 	
> 2. **Поиске** (`Collections.binarySearch`, `Arrays.binarySearch`).
> 	- `Arrays.binarySearch`:
> 	```java
> 	int index = Arrays.binarySearch(array, key); // Поиск индекса элемента
> 	```
> 	- `Collections.binarySearch`:
> 	```java
> 	int index = Collections.binarySearch(list, key);
> 	```
> 
> 3. **Коллекциях с естественным порядком**:
>     - `TreeSet` и `TreeMap`:
> 	```java
> 	TreeSet<Person> set = new TreeSet<>();
> 	set.add(new Person("Alice"));
> 	set.add(new Person("Bob"));
> 	```
> 	- `PriorityQueue`:
> 	```java
> 	PriorityQueue<Person> queue = new PriorityQueue<>();
> 	queue.add(new Person("Charlie"));
> 	```
> 
> 4. **Поиск минимальных/максимальных значений: **(`Collections.min`, `Collections.max`):
> 	```java
> 	Person min = Collections.min(list);
> 	Person max = Collections.max(list);
> 	```
> 	
> 5. **Потоковые данные (Stream API):**
> 	```java
> 	Optional<Person> minPerson = list.stream().min(Comparator.naturalOrder());
> 	Optional<Person> maxPerson = list.stream().max(Comparator.naturalOrder());
> 	```





<dir class="jcode" style="font-family: Consolas, monospace; font-size: 1rem; background-color: #f4f4f4; color: #333; padding: 1em; border-radius: 4px; box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1); white-space: pre-wrap; word-wrap: break-word; margin: 0;"> // Пример кода на Java">
#### Основное:
- Используется для естественной сортировки объектов.
- Сортировка определяется самим объектом, который реализует интерфейс.
- Метод: <code>compareTo(T o)</code> — **это единственный метод интерфейса** `Comparable` в Java, который используется для определения "естественного порядка" объектов. Он позволяет сравнивать текущий объект (`this`) с другим объектом (`o`) одного и того же типа `T`.
</dir>




> [!NOTE]
> 

> [!TIP]
> 

> [!WARNING]

> [!DANGER]

✅
⚠️
❗️
❌
🔴
🟠
🟤
🟣
🔵
🟡
🟢
⚪️
⚫️

><span style="font-size: 1.2em; font-weight: bold; margin: 0 !important; line-height: 1.2; display: inline-block; padding-bottom:0 !important; padding-left:0px !important;">**Чувствительность к регистру и локали**: </span>
>Метод не учитывает локаль
>
>*Например:*
><pre><code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px 5px; margin: 0px;">
> public class HelloWorld {
>	public static void main(String[] args) {
>		System.out.println("Hello, World!");
>	}
>}
></pre></code>
>Если требуется 
> <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding-top: 10px !important; padding-right: 10px !important; padding-bottom: 0px !important; padding-left: 10px !important; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
> <code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px ; margin: 0px;">
> import java.text.Collator;
> import java.util.Locale;
> </code>
> </pre>
> Если требуется  `Collator`:


|                                                                                                                                                                                                                                                              |                                                                                                                                                                                                                                                                                          |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Работа с одним типом данных:**<br>    <br>    - `switch` удобен для проверки значений типов `int`, `byte`, `short`, `char`, `String`, `enum`.<br>    - С новыми версиями Java поддерживаются строки и перечисления (`enum`), что делает его универсальным. | **Не фиксированные значения:**<br>    <br>    - Когда значения, с которыми сравнивается переменная, не фиксированы (например, вычисляются в процессе), `if-else` становится единственным вариантом.<br>- **Логические комбинации                                                         |
| <pre class="jcode"><br>public class HelloWorld {<br>    public static void main(String[] args) {<br>        System.out.println("Hello, World!");<br>    }<br>}<br></pre>                                                                                     | <pre class="jcode"><br>int day = 3;<br>    <br>switch (day) {<br>    case 1 -> System.out.println("Понедельник");<br>    case 2 -> System.out.println("Вторник");<br>    case 3 -> System.out.println("Среда");<br>    default -> System.out.println("Неизвестный день");<br>}<br></pre> |
| Какой то текст                                                                                                                                                                                                                                               | Какой то текст                                                                                                                                                                                                                                                                           |
|                                                                                                                                                                                                                                                              |                                                                                                                                                                                                                                                                                          |
<div style="height: 4px; background: linear-gradient(to right, #4facfe, #00f2fe); box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2); margin: 20px 0;"></div>








[^200]:1
[^201]:2


[^1]:
	Сноска

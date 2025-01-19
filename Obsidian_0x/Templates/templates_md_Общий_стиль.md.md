
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
><code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px 5px; margin: 0px;">
> System; // false
></code>
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

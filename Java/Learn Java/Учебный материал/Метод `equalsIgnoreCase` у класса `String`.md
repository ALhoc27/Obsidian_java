Метод `boolean equalsIgnoreCase(String anotherString)` — это встроенный метод в классе `String` в Java, предназначенный для сравнения двух строк **без учёта регистра**. Он возвращает `true`, если строки равны, игнорируя разницу между заглавными и строчными буквами.
##### Синтаксис:
```java
public boolean equalsIgnoreCase(String anotherString)
```
##### Возвращаемого значения:
- `true`, если строки равны по содержимому, игнорируя регистр.
- `false`, если строки отличаются по содержимому, или если `anotherString` равен `null`.
##### Как работает метод:
1. Если `anotherString` равен `null`, метод сразу возвращает `false`.
2. Если длины строк отличаются, метод возвращает `false`.
3. Каждый символ двух строк сравнивается, преобразуясь к одному регистру (обычно с использованием их значений в Unicode).
4. Если все символы равны, метод возвращает `true`.

**Пример кода**:
```java
public class EqualsIgnoreCaseExample {
    public static void main(String[] args) {
        String s1 = "Hello";
        String s2 = "hello";
        String s3 = "HELLO";
        String s4 = "World";

        System.out.println(s1.equalsIgnoreCase(s2)); // true, игнорируется разница между 'H' и 'h'
        System.out.println(s1.equalsIgnoreCase(s3)); // true, игнорируется разница между 'e' и 'E'
        System.out.println(s1.equalsIgnoreCase(s4)); // false, строки отличаются по содержимому
        System.out.println(s1.equalsIgnoreCase(null)); // false, anotherString = null
    }
}
```

### **Чувствительность к регистру и локали**:

Метод не учитывает локаль и просто сравнивает символы на основе их значений в Unicode после преобразования в нижний или верхний регистр. Например:
```java
System.out.println("ß".equalsIgnoreCase("SS")); // false
```
Если требуется сравнение с учётом локали, используйте `Collator` из пакета `java.text`:
```java
import java.text.Collator;
import java.util.Locale;

public class LocaleComparison {
    public static void main(String[] args) {
        Collator collator = Collator.getInstance(Locale.GERMAN);
        collator.setStrength(Collator.PRIMARY); // Игнорировать регистр и диакритические знаки

        System.out.println(collator.compare("ß", "ss") == 0); // true
    }
}
```




><span style="font-size: 1.2em; font-weight: bold; margin: 0 !important; line-height: 1.2; display: inline-block; padding-bottom:0 !important; padding-left:0px !important;"> &nbsp;&nbsp; **Чувствительность к регистру и локали**: </span>
>Метод не учитывает локаль и просто сравнивает символы на основе их значений в Unicode после преобразования в нижний или верхний регистр. Например:
>
><code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px 5px; margin: 0px;">
> System.out.println("ß".equalsIgnoreCase("SS")); // false
></code>Если требуется сравнение с учётом локали, используйте `Collator` из пакета `java.text`:
> <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 15px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
> <code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px 15px; margin: 0px;">
> import java.text.Collator;
> import java.util.Locale;
>  
> public class LocaleComparison {
> 	public static void main(String[] args) {
> 		Collator collator = Collator.getInstance(Locale.GERMAN);
> 		collator.setStrength(Collator.PRIMARY); // Игнорировать регистр и диакритические знаки
> 
> 		System.out.println(collator.compare("ß", "ss") == 0); // true
> 	}
> </code>
> </pre>
> f


evveve
veve
ev

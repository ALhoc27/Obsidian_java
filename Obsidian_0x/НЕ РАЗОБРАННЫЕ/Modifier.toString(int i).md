Метод `Modifier.toString(int mod)` преобразует числовое представление модификаторов (битовую маску) в строковое представление, которое легко читаемо человеком.
#### Сигнатура
```java
static String toString(int mod)
```

> [!NOTE]
> Метод **возвращает строковое представление модификаторов**, заданных в виде целого числа (битовой маски).
#### **Описание**
- **Параметр**:  
    `mod` — целое число, представляющее модификаторы в виде битовой маски.  
    Обычно его значение получают с помощью методов, таких как `getModifiers()` из классов `Class`, `Method`, `Field`, и других.
- **Возвращаемое значение**:  
    Строка, содержащая список модификаторов, разделённых пробелами. Например: `"public static final"`.
- **Модификаторы, которые может включать результат**:
    - `public`
    - `protected`
    - `private`
    - `abstract`
    - `static`
    - `final`
    - `synchronized`
    - `volatile`
    - `transient`
    - `native`
    - `strictfp`

<table class="language-java_td" style="width: 99%; border-collapse: collapse; margin-bottom: 5px;">
	<tr>
		<strong style="font-size: 1.1em; color: #333;">Пример :</strong>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333;"><span style="border: 1px solid black; padding: 2px;">#1</span>
&nbsp; Пример анализа модификаторов метода::</strong>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333;"><span style="border: 1px solid black; padding: 2px;">#2</span>
&nbsp; Пример №2:</strong>
        </td>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre class="language-java_td" style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
import java.lang.reflect.Method;
import java.lang.reflect.Modifier;
  
public class ModifierMethodExample {
    public static void main(String[] args) throws NoSuchMethodException {
        // Получаем метод класса
        Method method = Example.class.getMethod("exampleMethod");
  
        // Получаем модификаторы метода
        int modifiers = method.getModifiers();
 
        // Преобразуем модификаторы в строку
🔴      String result = Modifier.toString(modifiers);
  
        // Вывод: Modifiers of exampleMethod: public static final
        System.out.println("Modifiers of exampleMethod: " + result); 
    }
}
  
class Example {
    public static final void exampleMethod() {
        // Метод с модификаторами public static final
    }
}
				</code>
            </pre>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
import java.lang.reflect.Method;
import java.lang.reflect.Modifier;
  
public class Test {
    public static void main(String[] args) throws NoSuchMethodException {
        // Получаем класс
        Class＜SampleClass＞ clazz = SampleClass.class;
  
        // Получаем метод exampleMethod()
        Method method = clazz.getDeclaredMethod("exampleMethod");
  
        // Получаем модификаторы метода
        int modifiers = method.getModifiers();
  
        // Преобразуем модификаторы в строку
🔴      String modifierString = Modifier.toString(modifiers);
  
        // Выводим результат
        System.out.println("Модификаторы метода: " + modifierString);
    }
}
  
// Пример класса
class SampleClass {
    public static final synchronized void exampleMethod() {
        // Метод с несколькими модификаторами
    }
}
				</code>
            </pre>
        </td>
    </tr>
</table>

🔴 `Modifier.toString(int mod)` - Метод анализирует биты в числовом значении и добавляет в строку соответствующие модификаторы.

Простой пример для понимания данного метода - `Modifier.toString(int mod)`
```java
import java.lang.reflect.Modifier;  
  
public class Example {  
    void test() {  
🟠      int modifiers = Modifier.classModifiers();  
  
        // String result = Modifier.toString(modifiers);  
🟠      System.out.println("Допустимые модификаторы для классов: " + modifiers);  
    }  
  
    public static void main(String[] args) {  
        new Example().test();  
    }  
}
```
Без преобразования модификатора в строку методом `Modifier.toString(int mod)` мы получим просто число 🟠:
```yaml
Допустимые модификаторы для классов: 3103
```

### **Как работает `Modifier.toString(int mod)`**
Метод анализирует биты в числовом значении `mod` и добавляет в строку соответствующие модификаторы.
#### **Модификаторы и их битовые маски**
Каждый модификатор имеет уникальное значение (битовую маску), определённое в `Modifier`:
- `public` — `0x00000001` (1)
- `private` — `0x00000002` (2)
- `protected` — `0x00000004` (4)
- `static` — `0x00000008` (8)
- `final` — `0x00000010` (16)
- `synchronized` — `0x00000020` (32)
- `volatile` — `0x00000040` (64)
- `transient` — `0x00000080` (128)
- `native` — `0x00000100` (256)
- `interface` — `0x00000200` (512)
- `abstract` — `0x00000400` (1024)
- `strictfp` — `0x00000800` (2048)
#### **Алгоритм работы метода**
1. Метод последовательно проверяет, установлен ли соответствующий бит в значении `mod`.
2. Если бит установлен, добавляет в строку название модификатора.
3. Пробел используется как разделитель между модификаторами.

##### **Пример анализа модификаторов метода:**
```java
import java.lang.reflect.Method;
import java.lang.reflect.Modifier;

public class ModifierMethodExample {
    public static void main(String[] args) throws NoSuchMethodException {
        // Получаем метод класса
        Method method = Example.class.getMethod("exampleMethod");

        // Получаем модификаторы метода
        int modifiers = method.getModifiers();

        // Преобразуем модификаторы в строку
🔴      String result = Modifier.toString(modifiers);

        // Вывод результата
        System.out.println("Modifiers of exampleMethod: " + result); // Вывод: Modifiers of exampleMethod: public static final
    }
}

class Example {
    public static final void exampleMethod() {
        // Метод с модификаторами public static final
    }
}
```
Метод полезен для анализа кода во время выполнения (через рефлексию), чтобы определить, какие модификаторы используются для классов, методов или полей.
##### **Пример:**
```java
import java.lang.reflect.Modifier;

public class ModifierExample {
    public static void main(String[] args) {
🟣      int modifiers = Modifier.PUBLIC | Modifier.STATIC;

        // Преобразуем модификаторы в строку
🔵      String result = Modifier.toString(modifiers);

        System.out.println("Modifiers: " + result); // Вывод: public static
    }
}
```
###### **Объяснение:**
Этот метод анализирует битовую маску и возвращает соответствующую строку, например:
- Если модификатор — `public static`, то возвращается строка `"public static"`.
- Если модификаторов нет, возвращается пустая строка.
 🟣 [^2] 🔵 [^3]
###### Итоговый процесс выполнения кода:
1. Создаётся битовая маска([[Побитовые операции]]) для модификаторов `public` и `static`.
2. Битовая маска преобразуется в строку `"public static"` с помощью метода `Modifier.toString`.
3. Результат выводится на экран.
---

Разберём более сложный пример использования метода `static String toString(int mod)` из класса `Modifier`, чтобы показать, как он может применяться на практике для анализа модификаторов реальных классов и их компонентов.
##### Пример: Анализ модификаторов полей, методов и класса
```java
import java.lang.reflect.Method;
import java.lang.reflect.Modifier;
import java.lang.reflect.Field;

public class ModifierToStringExample {

    // Пример класса для анализа
    public static class ExampleClass {
        public static final int CONSTANT = 42;
        private String instanceVariable;

        public static void staticMethod() {}
        private void instanceMethod() {}
    }

    public static void main(String[] args) {
        try {
            // Получение объекта Class
            Class<?> clazz = ExampleClass.class;

            // Анализ модификаторов класса
            int classModifiers = clazz.getModifiers();
            System.out.println("Class Modifiers: " + Modifier.toString(classModifiers));

            // Анализ модификаторов полей
            Field[] fields = clazz.getDeclaredFields();
            for (Field field : fields) {
                int fieldModifiers = field.getModifiers();
                System.out.println("Field: " + field.getName() + ", Modifiers: " + Modifier.toString(fieldModifiers));
            }

            // Анализ модификаторов методов
            Method[] methods = clazz.getDeclaredMethods();
            for (Method method : methods) {
                int methodModifiers = method.getModifiers();
                System.out.println("Method: " + method.getName() + ", Modifiers: " + Modifier.toString(methodModifiers));
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
**Результат выполнения:**
```yaml
Class Modifiers: public static
Field: CONSTANT, Modifiers: public static final
Field: instanceVariable, Modifiers: private
Method: staticMethod, Modifiers: public static
Method: instanceMethod, Modifiers: private
```
###### Объяснение коду:
1. **Анализ модификаторов класса:**
    - `clazz.getModifiers()` возвращает битовую маску модификаторов класса `ExampleClass`.
    - `Modifier.toString(classModifiers)` преобразует маску в строку: `"public static"`. Это означает, что класс объявлен как `public` и `static`.
2. **Анализ модификаторов полей:**
    - Для каждого поля в классе `Field.getModifiers()` возвращает битовую маску.
    - Поле `CONSTANT` имеет модификаторы `public static final`, что отражается в строке.
    - Поле `instanceVariable` имеет модификатор `private`.
3. **Анализ модификаторов методов:**
    - Для каждого метода в классе `Method.getModifiers()` возвращает битовую маску.
    - Метод `staticMethod` имеет модификаторы `public static`.
    - Метод `instanceMethod` имеет модификатор `private`.
#### **Вывод (static String toString(int mod)):**
Метод `Modifier.toString(int mod)` чрезвычайно удобен для анализа модификаторов классов, методов, полей и конструкторов. Он позволяет легко преобразовать битовую маску модификаторов в человекочитаемую строку, что особенно полезно при использовании рефлексии для динамического анализа кода.
<br/><div style="text-align: center; margin: 0; padding: 0;"> <span style="color: #ff7e5f; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> <span style="color: #feb47b; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> <span style="color: #4facfe; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> </div>

[^2]:![[Снимок экрана 2025-01-11 в 14.56.02.png|450]]
	<hr/>
	
	```java
	int modifiers = Modifier.PUBLIC | Modifier.STATIC;
	```
	- **Создаём битовую маску модификаторов.**
	    - Здесь мы используем два модификатора: `Modifier.PUBLIC` и `Modifier.STATIC`.
	    - Каждый модификатор представлен как битовая константа:
	        - `Modifier.PUBLIC = 0x00000001` (значение 1)
	        - `Modifier.STATIC = 0x00000008` (значение 8)
	    - Оператор побитового ИЛИ (`|`) объединяет их в одно число:
	        - `modifiers = 0x00000001 | 0x00000008 = 0x00000009` (значение 9).
	
	**Результат:** переменная `modifiers` теперь содержит значение 9, которое соответствует модификаторам `public static`.

[^3]:
	![[Снимок экрана 2025-01-11 в 14.56.02.png|450]]
	<hr/>
	
	> [!NOTE] **Код в данном примере:** **Преобразовывает битовую маску модификаторов в строку.**
	>  ```java
	> String result = Modifier.toString(modifiers);
	> ```
	> 
	> - Метод `Modifier.toString(int mod)` анализирует битовую маску и возвращает строковое представление.
	> - `int modifiers` **в данном случае:** `public static` (***|** - является сложением в побитовых операциях*) = ...001 + ...008 =  `0x00000009`
	> - 
	>![[Снимок экрана 2025-01-13 в 02.13.07.png|200]]
	> - В метод `Modifier.toString(int mod)` мы передаем 
	> - **Значениe `modifiers` в данном случае равно 9, а это модификаторы 1(`public`) + 8(`static`) метод возвращает строку `"public static"`.**
	
	
	**Принцип работы `toString`:**
	- Метод проверяет каждый бит в числе `mod`:
	    - Если бит соответствует константе `Modifier.PUBLIC`, добавляется `"public"`.
	    - Если бит соответствует `Modifier.STATIC`, добавляется `"static"`.
	- Результат объединяется в строку с пробелами между модификаторами.
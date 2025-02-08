Класс `Modifier` в Java предоставляет методы для работы с модификаторами доступа и другими ключевыми словами, такими как `public`, `private`, `static`, `final` и так далее. Метод `classModifiers()` возвращает набор всех возможных модификаторов, которые могут применяться к классу.
#### Сигнатура
```java
public static int classModifiers()
```
- **Возвращаемое значение**: целое число (`int`), представляющее битовую маску допустимых модификаторов.
#### Возможные модификаторы классов:
1. **`public`** – класс доступен везде. [^1]
2. **`protected`** – класс доступен внутри пакета и подклассам вне пакета. ==**(только для вложенных классов)**== [^6]
3. **`private`** – класс доступен только внутри того же файла. ==**(только для вложенных классов)**== [^11]
4. **`abstract`** – класс является абстрактным и не может быть инстанцирован. [^3] 
5. **`static`** – используется для создания вложенных классов верхнего уровня.
6. **`final`** – класс нельзя наследовать. [^4]
7. **`strictfp`** – все вычисления с плавающей точкой должны соответствовать стандарту IEEE 754. [^5]

Метод `classModifiers()` из класса `java.lang.reflect.Modifier` возвращает целочисленное значение (в виде битовой маски), представляющее все **допустимые модификаторы для классов верхнего уровня и вложенных классов**. Эти модификаторы можно использовать, чтобы проверить или установить определенные свойства классов.

### **Недопустимые модификаторы для классов**
1. **`synchronized`**
    - Используется только для методов или блоков кода.
2. **`volatile`**
    - Применим только к переменным.
3. **`transient`**
    - Используется только для полей.
4. **`native`**
    - Применяется только к методам, реализованным на платформе вне Java.
5. **`private`** и **`protected`**
    - Неприменимы к классам верхнего уровня.
#### Пример использования
###### 1. Получить ==допустимые модификаторы классов==:
```java
import java.lang.reflect.Modifier;

public class Test {
    public static void main(String[] args) {
        // Получение допустимых модификаторов классов
        int modifiers = Modifier.classModifiers();

        // Вывод допустимых модификаторов
        System.out.println("Допустимые модификаторы классов: " + Modifier.toString(modifiers));
    }
}
```
**Вывод:**
```yaml
Допустимые модификаторы классов: public protected private abstract static final strictfp
```

2. **Кастомный класс**❗️
> [!WARNING] ВАЖНО!
> Метод `classModifiers()` из класса `java.lang.reflect.Modifier` **возвращает битовую маску всех допустимых модификаторов для классов**, а не модификаторы конкретного класса. Этот метод применяется для получения информации о допустимых модификаторах, которые можно использовать при объявлении класса.

> Если вы хотите проверить модификаторы конкретного кастомного класса, вы можете использовать метод `getModifiers()` из класса `Class` для получения модификаторов, а затем сравнить их с масками из класса `Modifier`.
> 
> Метод `classModifiers()` является статическим, и его можно вызывать напрямую через класс `Modifier`. Однако он возвращает только допустимую битовую маску, а не модификаторы конкретного класса. Если вы хотите использовать его для анализа кастомного класса, это можно сделать следующим образом:
```java
import java.lang.reflect.Modifier;

public class Test {
    public static void main(String[] args) {
        // Получение класса
        Class<?> clazz = CustomClass.class;

        // Получение модификаторов класса
        int modifiers = clazz.getModifiers();

        // Вывод модификаторов класса
        System.out.println("Модификаторы класса: " + Modifier.toString(modifiers));

        // Проверка конкретных модификаторов
        if (Modifier.isPublic(modifiers)) {
            System.out.println("Класс является public.");
        }
        if (Modifier.isAbstract(modifiers)) {
            System.out.println("Класс является abstract.");
        }
        if (Modifier.isFinal(modifiers)) {
            System.out.println("Класс является final.");
        }
    }
}

// Пример кастомного класса
public final class CustomClass {
}
```
**Вывод:**
```yaml
Модификаторы класса: public final
Класс является public.
Класс является final.
```
#### **Объяснение**
1. **`Modifier.classModifiers()`**  
    Возвращает битовую маску для допустимых модификаторов классов (например, `public`, `abstract`, `final`, и т.д.). ^[**Метод `classModifiers()`** возвращает комбинацию допустимых модификаторов для классов.]
2. **`clazz.getModifiers()`**  
    Получает модификаторы конкретного класса в виде целого числа (битовой маски).
3. **`Modifier.toString(int mod)`**  
    Преобразует битовую маску модификаторов в строку (например, `"public final"`).
4. **Проверка модификаторов**  
    Методы `Modifier.isPublic(int mod)`, `Modifier.isAbstract(int mod)`, и другие используются для проверки наличия конкретного модификатора.
#### **Вывод**
Для вызова `classModifiers()` у кастомного класса нет необходимости. Вместо этого используйте:
1. `Modifier.classModifiers()` — чтобы узнать все допустимые модификаторы.
2. `clazz.getModifiers()` — чтобы узнать модификаторы конкретного класса.

<br/><div style="text-align: center; margin: 0; padding: 0;"> <span style="color: #ff7e5f; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> <span style="color: #feb47b; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> <span style="color: #4facfe; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> </div>

[^1]:
	#### Для классов верхнего уровня
	`public` - Класс доступен из любого места в программе.
	
	**Пример:**
	```java
	public class MyClass {
	    // Код класса
	}
	```
	#### Для вложенных классов
	`public` - Делает вложенный класс доступным из любого места, где доступен внешний класс.
	
	**Пример:**
	```java
	public class OuterClass {
	    public class InnerClass {
	        // Код вложенного класса
	    }
	}
	```
	---
	> 
	> **Нестатический вложенный класс** (внутренний класс) также **==может==** быть объявлен с модификатором `public`
	> ```java
	> public class OuterClass {
	>     public class PublicInnerClass {
	>         public void display() {
	>             System.out.println("Я публичный внутренний класс!");
	>         }
	>     }
	> }
	> 
	> public class Test {
	>     public static void main(String[] args) {
	>         OuterClass outer = new OuterClass();
	>         OuterClass.PublicInnerClass inner = outer.new PublicInnerClass();
	>         inner.display();
	>     }
	> }
	> ```
	> **Локальные классы** (определяются внутри метода) **==не могут==** быть объявлены с модификатором `public`. Их область видимости ограничена блоком, где они определены.
	> ```java
	> public class OuterClass {
	>     public void method() {
	>         class LocalClass {
	>             void display() {
	>                 System.out.println("Я локальный класс!");
	>             }
	>         }
	>         LocalClass local = new LocalClass();
	>         local.display();
	>     }
	> }
	> 
	> public class Test {
	>     public static void main(String[] args) {
	>         OuterClass outer = new OuterClass();
	>         outer.method();
	>     }
	> }
	> ```

[^2]:```

[^3]:#### Для классов верхнего уровня
	`abstract` - Указывает, что класс является абстрактным и не может быть инстанцирован.  
	Может содержать абстрактные методы (без реализации).
	**Пример:**
	```java
	public abstract class AbstractClass {
	    abstract void myMethod();
	}
	```
	
	#### Для вложенных классов
	`abstract` - Указывает, что вложенный класс является абстрактным.
	
	**Пример:**
	```java
	public class OuterClass {
	    final class InnerClass {
	        // Код вложенного класса
	    }
	}
	```
[^4]:**Пример:**
	```java
	public final class FinalClass {
	    // Код класса
	}
	```
	
	**Пример:**
	```java
	public class OuterClass {
	    final class InnerClass {
	        // Код вложенного класса
	    }
	}
	```
[^5]:**Пример:**
	```java
	public strictfp class StrictfpClass {
	    // Код класса
	}
	```
	
[^6]:#### `protected` - **(только для вложенных классов)**
	Класс доступен внутри пакета и подклассам вне пакета.
	**Пример:**
	```java
	public class OuterClass {
	    protected class InnerClass {
	        // Код вложенного класса
	    }
	}
	```

[^8]:#### Для вложенных классов
	`abstract` - Указывает, что вложенный класс является абстрактным.
	
	**Пример:**
	```java
	public class OuterClass {
	    final class InnerClass {
	        // Код вложенного класса
	    }
	}
	```

[^11]:#### `private` - **(только для вложенных классов)**
	Класс доступен только внутри файла, где он объявлен (для вложенных классов).
	**Пример:**
	```java
	public class OuterClass {
	    private class PrivateInnerClass {
	        // Код
	    }
	}
	```

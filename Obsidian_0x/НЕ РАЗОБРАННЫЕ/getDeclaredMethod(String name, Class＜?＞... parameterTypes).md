#### **Метод `getDeclaredMethod(String name, Class<?>... parameterTypes)`**
Этот метод класса `Class` позволяет получить объект `Method`, представляющий метод с определенным именем и сигнатурой, объявленный в самом классе. Метод может быть **приватным**, **защищенным**, **пакетным** или **публичным**.
#### Сигнатура метода
```java
public Method getDeclaredMethod(String name, Class<?>... parameterTypes) throws NoSuchMethodException, SecurityException
```
#### **Аргументы:**
1. **`name`**:  
    Строка, представляющая имя метода, который вы хотите получить.
2. **`parameterTypes`**:  
    Список классов параметров метода в порядке их следования.
#### **Возвращаемое значение:**
- Объект `Method`, представляющий метод с указанным именем и параметрами.

#### **Исключения:**
1. **`NoSuchMethodException`**:  
    Бросается, если метод с указанным именем и параметрами не найден.
2. **`SecurityException`**:  
    Бросается, если текущий контекст безопасности не позволяет получить доступ к методу.

#### **Особенности:**
- Этот метод работает только с методами, объявленными непосредственно в указанном классе. ()
- Не включает методы, унаследованные от суперклассов.
- Может использоваться для доступа к приватным методам.
- Для вызова приватного метода необходимо сначала установить доступность через `setAccessible(true)`.

#### **Примеры использования**
##### 1. Получение публичного метода
```java
import java.lang.reflect.Method;

class Example {
    public void sayHello(String name) {
        System.out.println("Hello, " + name + "!");
    }
}

public class Main {
    public static void main(String[] args) throws Exception {
        Class<?> clazz = Example.class;

        // Получение метода sayHello
        Method method = clazz.getDeclaredMethod("sayHello", String.class);

        // Вызов метода
        Example example = new Example();
        method.invoke(example, "Alice"); // Hello, Alice!
    }
}
```
##### 2. Получение приватного метода
```java
public class Example {  
    private void secretMessage(String str) {  
        System.out.println(str);  
    }  
}  
  
 class Main {  
    public static void main(String[] args) throws Exception {  
        Class<?> clazz = Example.class;  
  
        // Получение приватного метода  
        Method method = clazz.getDeclaredMethod("secretMessage", String.class);  
  
        // Делаем метод доступным  
        method.setAccessible(true);  
  
        // Вызов метода  
        Example example = new Example();  
        method.invoke(example, "This is a secret method!"); // This is a secret method!
    }  
}
```
Метод `invoke()` описан в ([[java.lang.reflect.Method#Основные методы класса `Method`]])
##### 3. Работа с перегруженными методами
Если в классе объявлено несколько методов с одинаковым именем, нужно указать правильные параметры, чтобы получить нужный метод.
```java
import java.lang.reflect.Method;

class Example {
    public void print(int number) {
        System.out.println("Number: " + number);
    }

    public void print(String message) {
        System.out.println("Message: " + message);
    }
}

public class Main {
    public static void main(String[] args) throws Exception {
        Class<?> clazz = Example.class;l;

        // Получение метода print(int)
        Method methodInt = clazz.getDeclaredMethod("print", int.class);
        Method methodString = clazz.getDeclaredMethod("print", String.class);

        // Вызов методов
        Example example = new Example();
        methodInt.invoke(example, 42);
        methodString.invoke(example, "Hello");
    }
}
```
**Вывод**:
```yaml
Number: 42 
Message: Hello
```

> [!TIP]
> #### **Различия с `getMethod`**
> - `getMethod`: Ищет **только публичные методы**, включая унаследованные.
> - `getDeclaredMethod`: Ищет **любые методы**, но **только объявленные в данном классе**.
#### **Итог**
Метод `getDeclaredMethod` является мощным инструментом для работы с методами класса, особенно если требуется доступ к защищенным или приватным методам. Однако его использование должно быть оправдано, так как это обход стандартного механизма инкапсуляции.
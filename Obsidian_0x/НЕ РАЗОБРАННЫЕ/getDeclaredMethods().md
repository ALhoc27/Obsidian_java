Метод **`getDeclaredMethods()`** класса [[java.lang.Class<T>]] в Java используется для получения всех методов(**включая `private`**), которые были **объявлены непосредственно в классе**. Он возвращает массив объектов типа `Method`, представляющих все методы, которые находятся в текущем классе, включая методы с любым уровнем доступа (`private`, `protected`, `package-private`, и `public`).
#### Сигнатура метода:
```java
public Method[] getDeclaredMethods()
```
#### Возвращаемое значение: 
Этот метод возвращает массив объектов `Method`, представляющих все методы, объявленные в текущем классе. В отличие от метода `getMethods()`, `getDeclaredMethods()` включает в себя все методы класса, независимо от их уровня доступа, включая приватные и защищенные методы, ==но **не включает унаследованные методы==**.
#### Особенности:
- **Включает все методы, объявленные в текущем классе**: независимо от их модификаторов доступа (`public`, `private`, `protected`, или `package-private`).
- **==Не включает унаследованные методы==**: метод возвращает только те методы, которые были определены непосредственно в этом классе. Методы, унаследованные от суперклассов, не включаются.
- Может использоваться для анализа или манипуляций с приватными методами (если вы используете `setAccessible(true)`).

***Пример использования метода** `getDeclaredMethods()`*
Предположим, у нас есть класс с несколькими методами с разными уровнями доступа.
```java
import java.lang.reflect.Method;

class Example {
    public void publicMethod() {
        System.out.println("public method");
    }

    private void privateMethod() {
        System.out.println("private method");
    }

    protected void protectedMethod() {
        System.out.println("protected method");
    }

    void packagePrivateMethod() {
        System.out.println("package-private method");
    }
}

public class Main {
    public static void main(String[] args) {
        try {
            // Получаем объект Class для Example
            Class<?> clazz = Example.class;

            // Получаем все методы, объявленные в классе
            Method[] methods = clazz.getDeclaredMethods();

            // Перебираем и выводим имена методов
            for (Method method : methods) {
                System.out.println("Метод: " + method.getName());
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
**Результат выполнения:**
```yaml
Метод: publicMethod
Метод: privateMethod
Метод: protectedMethod
Метод: packagePrivateMethod
```
#### Что происходит в примере:
- Мы создаем класс `Example` с четырьмя методами, каждый с разным модификатором доступа.
- В методе `main` мы используем **`getDeclaredMethods()`**, чтобы получить все методы, объявленные в классе `Example`.
- Метод `getDeclaredMethods()` возвращает массив объектов `Method`, который мы затем перебираем и выводим имена(`getName()`) всех найденных методов.
#### Работа с приватными методами:
Если вы хотите вызвать приватный метод, вам нужно использовать метод `setAccessible(true)` для каждого метода, полученного с помощью `getDeclaredMethods()`, чтобы сделать его доступным для рефлексии.

**Пример вызова приватного метода:**
```java
import java.lang.reflect.Method;

class Example {
    private void privateMethod() {
        System.out.println("This is a private method");
    }
}

public class Main {
    public static void main(String[] args) {
        try {
            Class<?> clazz = Example.class;

            // Получаем приватный метод
🔵          Method method = clazz.getDeclaredMethod("privateMethod");

            // Делаем метод доступным
🟠          method.setAccessible(true);

            // Создаем объект и вызываем метод
            Example example = new Example();
🟣          method.invoke(example); // вызываем метод
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
[[java.lang.reflect.Method#Основные методы класса `Method`]]
**Результат:**
```yaml
This is a private method
```

> [!DANGER] Title
> ### **Важные моменты:**
> 
> - Метод **`getDeclaredMethods()`** не возвращает унаследованные методы. Чтобы получить все методы, включая унаследованные, нужно использовать **`getMethods()`**. [[getMethods()]]
> - Для работы с приватными или защищенными методами, которые были получены с помощью `getDeclaredMethods()`, вам нужно установить доступность метода через `setAccessible(true)`. Это необходимо, чтобы обойти ограничения доступа и использовать метод.

![[Снимок экрана 2025-01-06 в 02.03.49.png|650]]
#### **Рекомендации по использованию:**
- **`getDeclaredMethods()`** полезен, когда вам нужно получить полный список методов, определенных в текущем классе, включая приватные методы, но без учета методов, унаследованных от суперклассов.
- Для работы с приватными методами используйте `setAccessible(true)`.
- Если вам нужны только публичные методы, лучше использовать `getMethods()`.
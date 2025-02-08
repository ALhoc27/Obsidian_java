#### Метод `getParameterTypes()` класса `Method`
Метод `getParameterTypes()` из класса `java.lang.reflect.Method` **==возвращает массив** объектов типа `Class<?>`, представляющих параметры метода==. Это позволяет узнать, какие типы данных принимает метод.
#### Сигнатура метода
```java
public Class<?>[] getParameterTypes()
```
#### Описание
> - Возвращает массив `Class<?>`, где каждый элемент массива соответствует типу одного из параметров метода в порядке их объявления.
> - Если метод не принимает параметров, возвращается пустой массив.

---
#### Пример использования
Допустим, у нас есть класс с несколькими методами:
```java
class Example {
    public void method1(int a, String b) {}
    public void method2() {}
    private void method3(double c, boolean d) {}
}
```
Теперь мы можем использовать `getParameterTypes()` для анализа параметров этих методов:
```java
import java.lang.reflect.Method;

public class Main {
    public static void main(String[] args) {
        try {
            // Получаем методы класса Example
🟣          Method[] methods = Example.class.getDeclaredMethods();

            for (Method method : methods) {
                System.out.println("Метод: " + method.getName());

                // Получаем типы параметров
🟠              Class<?>[] parameterTypes = method.getParameterTypes();

                if (parameterTypes.length == 0) {
                    System.out.println("  Параметры: отсутствуют");
                } else {
                    System.out.print("  Параметры: ");
                    for (Class<?> paramType : parameterTypes) {
                        System.out.print(paramType.getName() + " ");
                    }
                    System.out.println();
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
**Результат выполнения**
```yaml
Метод: method1
  Параметры: int java.lang.String 
Метод: method2
  Параметры: отсутствуют
Метод: method3
  Параметры: double boolean 
```
#### Объяснение работы
1. **Получение методов**: Мы используем `getDeclaredMethods()` для получения всех методов, включая приватные.
2. **Получение типов параметров**: Для каждого метода вызываем `getParameterTypes()`:
    - Если метод принимает параметры, массив будет содержать их типы.
    - Если параметров нет, возвращается пустой массив.
#### Особенности
1. **Типы примитивов**: Если метод принимает примитивные типы, массив будет содержать соответствующие классы примитивов (например, `int`, `double`, `boolean`).
2. **Параметры-ссылки**: Если метод принимает ссылочные типы, например `String` или `List`, массив будет содержать объекты `Class` этих типов, такие как `java.lang.String` или `java.util.List`.
3. **Массивы**: Если метод принимает массив, например `int[]`, то `getParameterTypes()` вернет `int[]`.

**Пример с методом, принимающим массивы**
```java
class ArrayExample {
    public void processArray(int[] numbers, String[][] data) {}
}

public class Main {
    public static void main(String[] args) throws Exception {
        Method method = ArrayExample.class.getMethod("processArray", int[].class, String[][].class);

        Class<?>[] parameterTypes = method.getParameterTypes();

        for (Class<?> paramType : parameterTypes) {
            System.out.println("Параметр: " + paramType.getName());
        }
    }
}
```
**Результат:**
```yaml
Параметр: [I
Параметр: [[Ljava.lang.String;
```

Объяснение результата:
- `[I` — обозначает массив типа `int[]`.
- `[[Ljava.lang.String;` — обозначает двумерный массив типа `String[][]`.

#### Когда использовать `getParameterTypes()`
- Для анализа сигнатуры метода (например, в фреймворках или инструментах для тестирования).
- Для динамического вызова методов, где необходимо определить типы параметров перед передачей аргументов.
- В рефлексивных утилитах, чтобы определить совместимость параметров метода с передаваемыми аргументами.

---
#### Ограничения
- Этот метод не учитывает информацию о типах параметров с использованием дженериков. Например, для `List<String>` он вернет только `java.util.List`, без уточнения дженерика `<String>`. Для такой информации нужно использовать `java.lang.reflect.Parameter` или `java.lang.reflect.Type` в Java 8 и выше.
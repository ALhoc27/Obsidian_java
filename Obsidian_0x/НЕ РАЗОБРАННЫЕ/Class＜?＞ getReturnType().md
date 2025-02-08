Метод `getReturnType()` класса `Method` используется для получения объекта `Class`, который представляет тип возвращаемого значения метода. Этот метод полезен, когда вы работаете с рефлексией и хотите узнать, какой тип данных возвращает метод.
#### Сигнатура
```java
public Class<?> getReturnType()
```
#### Описание
- Возвращает объект `Class`, который представляет тип возвращаемого значения метода.
- Если метод возвращает примитивный тип (например, `int`, `boolean`), то возвращается соответствующий класс-обертка (например, `int.class`, `boolean.class`).
- Если метод возвращает `void`, то возвращается `void.class`.
#### Пример использования
```java
import java.lang.reflect.Method;

class Example {
	public int add(int a, int b) {
		return a + b;
	}

	public void display() {
		System.out.println("This is a void method");
	}
}

public class Main {
	public static void main(String[] args) {
		try {
			// Получаем объект класса
			Class<?> clazz = Example.class;

			// Получаем методы
			Method addMethod = clazz.getMethod("add", int.class, int.class);
			Method displayMethod = clazz.getMethod("display");

			// Получаем возвращаемые типы
🟤			Class<?> returnTypeAdd = addMethod.getReturnType();
🟤			Class<?> returnTypeDisplay = displayMethod.getReturnType();

			// Вывод информации
			System.out.println("Return type of 'add': " + returnTypeAdd.getName()); // Return type of 'add': int
			System.out.println("Return type of 'display': " + returnTypeDisplay.getName()); // Return type of 'display': void
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```
#### Объяснение
1. **`getReturnType()`**:
	- Для метода `add` возвращает `int.class`.
	- Для метода `display` возвращает `void.class`.
2. **`Class.getName()`**:
	- Преобразует объект `Class` в строковое представление имени типа. [[java.lang.Class<T>#Описание основных методов с примерами]]
---
#### Применение
- **Динамический вызов методов**: Используется для проверки типа возвращаемого значения перед его использованием.
- **Сериализация/десериализация**: Позволяет определить возвращаемый тип метода при создании универсальных решений для сериализации.
- **Анализ классов**: Полезен для генерации документации или анализа структуры кода.
---
#### Особенности
- Для массивов возвращает объект `Class`, представляющий массив (например, `int[].class`).
- Для обобщённых типов возвращает `Class` базового типа (например, для `List<String>` вернёт `List.class`).

#### Пример для метода с массивом:
```java
class Example {
	public int[] getArray() {
		return new int[]{1, 2, 3};
	}
}

public class Main {
	public static void main(String[] args) throws Exception {
		Method method = Example.class.getMethod("getArray");
🟤		System.out.println("Return type: " + method.getReturnType().getName()); // Вывод: [I
	}
}
```
`[I` — это внутреннее представление типа массива `int[]`.
#### Особый случай: Примитивы и обертки
Если метод возвращает примитивный тип, то `getReturnType()` вернёт его представление в `Class`. Например:
- `int` → `int.class`
- `boolean` → `boolean.class`
Если возвращаемое значение — объект, то вернётся соответствующий класс.

---
#### Ошибки и исключения
- **Нет исключений**: Метод `getReturnType()` не бросает исключений. Вызывается для объекта `Method`, который уже корректно получен.
	
	
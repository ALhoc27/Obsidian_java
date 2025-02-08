Метод `invoke(Object obj, Object... args)` класса `java.lang.reflect.Method` используется для вызова метода через рефлексию. Этот метод позволяет динамически вызывать методы объекта во время выполнения программы, даже если на этапе компиляции о них ничего не известно.
##### Сигнатура метода
```java
Object invoke(Object obj, Object... args) throws IllegalAccessException, IllegalArgumentException, InvocationTargetException
```
##### ==Описание параметров==
- **`obj`**: ==**объект, на котором вызывается метод**. Если метод статический, `obj` может быть `null`.==
- **`args`**: ==**массив аргументов, передаваемых методу**. Если у метода нет параметров, передается пустой массив или `null`.==
##### Возвращаемое значение
- **Объект**: результат выполнения метода, если метод что-то возвращает.
- Если метод возвращает `void`, то метод `invoke` возвращает `null`.
##### Исключения
- **`IllegalAccessException`**: если доступ к методу запрещен (например, метод приватный и доступ не был установлен). [[Доступ к private методу (Рефлексия)]]
- **`IllegalArgumentException`**: если переданы неподходящие аргументы.
- **`InvocationTargetException`**: если вызванный метод выбрасывает исключение, оно оборачивается в `InvocationTargetException`.
#### **Особенности**
- Для вызова приватных методов нужно предварительно сделать метод доступным, вызвав `setAccessible(true)`.
- Типы аргументов должны совпадать с сигнатурой метода, иначе возникнет ошибка.

### **Примеры использования**
##### 1. Вызов публичного метода
```java
import java.lang.reflect.Method;

class Example {
	public void printMessage(String message) {
		System.out.println("Message: " + message);
	}
}

public class Main {
	public static void main(String[] args) throws Exception {
		Example example = new Example();

		// Получение объекта Method
		Method method = Example.class.getMethod("printMessage", String.class);

		// Вызов метода через рефлексию
🟣      method.invoke(example, "Hello, Reflection!");
	}
}
```
**Результат**:
```yaml
Message: Hello, Reflection!
```

##### 2. Вызов статического метода
```java
import java.lang.reflect.Method;

class Example {
	public static void staticMethod() {
		System.out.println("Static method called");
	}
}

public class Main {
	public static void main(String[] args) throws Exception {
		// Получение объекта Method
		Method method = Example.class.getMethod("staticMethod");

		// Вызов статического метода (obj = null)
🟣      method.invoke(null);
	}
}
```
**Результат**:
```yaml
Static method called
```

##### 3. Вызов метода с несколькими параметрами
```java
import java.lang.reflect.Method;

class Example {
	public int sum(int a, int b) {
		return a + b;
	}
}

public class Main {
	public static void main(String[] args) throws Exception {
		Example example = new Example();

		// Получение объекта Method
		Method method = Example.class.getMethod("sum", int.class, int.class);

		// Вызов метода через рефлексию
🟣      Object result = method.invoke(example, 5, 10);

		// Вывод результата
		System.out.println("Result: " + result);
	}
}
```
**Результат**:
```yaml
Result: 15
```
##### 4. Вызов приватного метода
```java
import java.lang.reflect.Method;

class Example {
	private void privateMethod() {
		System.out.println("Private method called");
	}
}

public class Main {
	public static void main(String[] args) throws Exception {
		Example example = new Example();

		// Получение объекта Method
		Method method = Example.class.getDeclaredMethod("privateMethod");

		// Открываем доступ к приватному методу
		method.setAccessible(true);

		// Вызов метода
🟣	    method.invoke(example);
	}
}
```
**Результат**:
```yaml
Private method called
```
##### 5. Обработка исключений `InvocationTargetException`
```java
import java.lang.reflect.Method;

class Example {
	public void throwException() throws Exception {
		throw new Exception("An exception occurred");
	}
}

public class Main {
	public static void main(String[] args) {
		try {
			Example example = new Example();

			// Получение объекта Method
			Method method = Example.class.getMethod("throwException");

			// Вызов метода
🟣			method.invoke(example);
		} catch (Exception e) {
			// Вывод исходного исключения
			Throwable cause = e.getCause();
			System.out.println("Caught exception: " + cause.getMessage());
		}
	}
}
```
**Результат**:
```yaml
Caught exception: An exception occurred
```
##### 6. Вызов метода с массивом параметров 
```java
import java.lang.reflect.Method;

class Example {
	public void printArray(String[] arr) {
		for (String s : arr) {
			System.out.println(s);
		}
	}
}

public class Main {
	public static void main(String[] args) throws Exception {
		Example example = new Example();

		// Получение объекта Method
		Method method = Example.class.getMethod("printArray", String[].class);

		// Вызов метода
		String[] data = {"one", "two", "three"};
🟣		method.invoke(example, (Object) data);
	}
}
```
**Результат**:
```yaml
one
two
three
```
[[Приведения аргументов (масива) к типу Object (Рефлексия)]]
##### Почему приводим к (Object)
> Массивы в Java — это объекты, и они могут быть переданы как одно целое в методы, которые принимают параметр типа `Object`. Однако, при использовании рефлексии и передачи массива в метод с переменным числом аргументов (`Object... args`), Java может интерпретировать его как множество отдельных элементов, а не как один объект (массив).
>
> Приведение массива к `Object` позволяет избежать путаницы и гарантирует, что массив передан как единый объект, а не распаковывается в отдельные элементы.

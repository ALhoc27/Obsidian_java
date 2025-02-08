Метод **`getMethod(String name, Class＜?＞... parameterTypes)`** принадлежит классу **`Class`** ([[java.lang.Class<T>]]) и предназначен для получения объекта `Method`, который представляет **публичный метод** указанного класса или его суперклассов. Этот метод позволяет работать с методами рефлексивно, передавая имя метода и его параметры.
```java
public Method getMethod(String name, Class<?>... parameterTypes) throws NoSuchMethodException, SecurityException
```
**Описание:** Возвращает объект `Method` для ==**публичного метода**==, объявленного в текущем классе или унаследованного от суперклассов.  
#### **Параметры:**
1. **`name`** - **имя метода, который нужно найти.**
	- Тип: `String`
	- Имя метода, который нужно найти.
	- Учитывает регистр букв (чувствителен к регистру).
2. **`parameterTypes`**
	- Тип: `Class<?>...` (массив типов параметров метода).
	- Определяет типы аргументов метода в точности, включая порядок.
	- Если метод не принимает аргументов, передайте пустой массив (`new Class<?>[0]` или ничего).
#### **Исключения:**
- **`NoSuchMethodException`**  
	Выбрасывается, если метод с указанным именем и параметрами не найден.
- **`SecurityException`**  
	Выбрасывается, если к методу невозможно получить доступ из-за настроек безопасности.
#### **Возвращаемое значение:**
- Объект `Method`, представляющий найденный метод.
#### **Особенности:**
- Возвращает только **публичные** методы текущего класса или его суперклассов.  
	Приватные и защищенные методы **не возвращаются** этим методом.
- Если метод переопределен в суперклассе, возвращается версия из текущего класса.
- Если метод принадлежит интерфейсу, он также может быть найден.
- Проверяет соответствие имени и типов параметров.

**Пример 1: Получение и вызов метода ==без параметров**==
Класс `Example` содержит публичный метод `display`.  
Мы получаем объект `Method` для этого метода и вызываем его с помощью `invoke` ([[java.lang.reflect.Method#Основные методы класса `Method`]]).
```java
import java.lang.reflect.Method;

class Example {
	public void display() {
		System.out.println("Метод display вызван!");
	}
}

public class Main {
	public static void main(String[] args) {
		try {
			// Получаем объект Method для метода display
			Method method = Example.class.getMethod("display");

			// Вызываем метод
			method.invoke(new Example());
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```
**Вывод:**
```yaml
Метод display вызван!
```

**Пример 2: Получение и вызов метода ==с параметрами**==
Класс `Calculator` содержит метод `add`, который принимает два параметра типа `int`. [[java.lang.reflect.Method#Основные методы класса `Method`]]
```java
import java.lang.reflect.Method;

class Calculator {
	public int add(int a, int b) {
		return a + b;
	}
}

public class Main {
	public static void main(String[] args) {
		try {
			// Получаем объект Method для метода add(int, int)
			Method method = Calculator.class.getMethod("add", int.class, int.class);

			// Вызываем метод
			Object result = method.invoke(new Calculator(), 5, 7);
			System.out.println("Результат: " + result);
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```
**Вывод:**
```yaml
Результат: 12
```

**Пример 3: Метод в суперклассе**
Метод `toString` унаследован от класса `Object`.
```java
import java.lang.reflect.Method;

class Example {}

public class Main {
	public static void main(String[] args) {
		try {
			// Получаем объект Method для метода toString из суперкласса
			Method method = Example.class.getMethod("toString");

			// Вызываем метод
			Object result = method.invoke(new Example());
			System.out.println("Результат: " + result);
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```
#### Разберем пример 3
##### Класс `Example`
```java
class Example {}
```
- Это пустой класс, который не переопределяет никаких методов.
- Однако, как и любой другой класс в Java, он неявно наследуется от класса `Object`, что делает методы `Object` (включая `toString`) доступными для экземпляров `Example`.
##### Основной метод `main`
```java
Method method = Example.class.getMethod("toString");
```
- Метод `getMethod` используется для получения объекта `Method`, представляющего публичный метод `toString`, объявленный в классе `Object`.
- Поскольку `Example` не переопределяет `toString`, будет возвращен метод `toString` суперкласса `Object`.
```java
Object result = method.invoke(new Example());
```
- Метод `invoke` используется для вызова метода `toString` для объекта `new Example()`.
- Вызов `toString` в данном случае будет использовать реализацию из класса `Object`, которая возвращает строку в формате `<Имя_класса>@<хеш-код>`.
```java
System.out.println("Результат: " + result);
```
Результат вызова метода `toString` выводится на экран.
##### Обработка исключений
```java
catch (Exception e) {
    e.printStackTrace();
}
```
Любая ошибка, возникающая при рефлексии (например, `NoSuchMethodException`, `IllegalAccessException`, или `InvocationTargetException`), будет поймана и напечатана в консоль.

**Результат выполнения кода:**
```java
Результат: Example@<хеш-код>
```
- `<хеш-код>` — это хеш-код объекта, представленный в шестнадцатеричном формате.

##### <span style="border: 1px solid black; padding: 2px;">Расширение примера</span>
==Если== добавить собственную реализацию `toString` в `Example`, результат изменится:
```java
class Example {
    @Override
    public String toString() {
        return "Custom toString() implementation";
    }
}
```
**Результат программы:**
```yaml
Результат: Custom toString() implementation
```
Теперь метод `invoke` вызовет новую реализацию `toString`.
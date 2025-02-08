Класс `Method` из пакета `java.lang.reflect` предоставляет методы для работы с методами классов, включая их извлечение, анализ и вызов. Он является частью рефлексии в Java и позволяет взаимодействовать с методами классов во время выполнения.
#### Сигнатура:
```java
public final class Method extends Executable
```
Класс **`Method`** наследуется от **`Executable`**, который также является родителем класса **`Constructor`**.
#### **Как получить объект `Method`?**
Для получения объекта `Method` используются ==методы класса== `Class`:
1. **`getMethods()`**: Возвращает массив всех публичных методов текущего класса и его суперклассов. **(==Только публичные методы==)** [[getMethods()]]
2. **`getMethod(String name, Class<?>... parameterTypes)`**: Возвращает публичный метод с указанным именем и параметрами. [[getMethod(String name, Class＜?＞... parameterTypes)]]
3. **`getDeclaredMethods()`**: Возвращает массив всех методов текущего класса, включая `private`. **(Все методы, включая `private`)** [[getDeclaredMethods()]]
4. **`getDeclaredMethod(String name, Class<?>... parameterTypes)`**: Возвращает метод с указанным именем и параметрами, включая `private`. [[getDeclaredMethod(String name, Class＜?＞... parameterTypes)]]

#### Основные методы класса `Method`

| Метод                                         | Описание                                                                                 |
| --------------------------------------------- | ---------------------------------------------------------------------------------------- |
| [[Object invoke(Object obj, Object... args)]] | Вызывает метод с указанными аргументами.                                                 |
| [[Class＜?＞ getReturnType()]]                  | Возвращает тип возвращаемого значения у метода.                                          |
| [[Class＜?＞[] getParameterTypes()]]            | Возвращает массив типов параметров метода.                                               |
| [[int getModifiers()]]`                       | Возвращает модификаторы метода (например, `public`, `private`, `static`).                |
| `Annotation[] getAnnotations()`               | Возвращает массив всех аннотаций, связанных с методом.                                   |
| `Annotation[][] getParameterAnnotations()`    | Возвращает аннотации параметров метода в виде двумерного массива.                        |
| `String getName()`                            | Возвращает имя метода.                                                                   |
| `boolean isAccessible()`                      | Проверяет, доступен ли метод для вызова (устарел с Java 9).                              |
| `void setAccessible(boolean flag)`            | Устанавливает доступ к методу (включая приватные) (устарел с Java 9).                    |
| `boolean isDefault()`                         | Проверяет, является ли метод `default` (в интерфейсе).                                   |
| `boolean isSynthetic()`                       | Проверяет, является ли метод синтетическим (созданным компилятором, а не разработчиком). |
| `Type getGenericReturnType()`                 | Возвращает тип возвращаемого значения с учетом параметризации.                           |
| `Type[] getGenericParameterTypes()`           | Возвращает массив параметризованных типов параметров метода.                             |
<br/>
<div style="text-align: center; margin: 0; padding: 0;"> <span style="color: #ff7e5f; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> <span style="color: #feb47b; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> <span style="color: #4facfe; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> </div>



[^5]:```java
	public Method getMethod(String name, Class<?>... parameterTypes) throws NoSuchMethodException, SecurityException
	```
	- **Описание:** Возвращает объект `Method` для ==**публичного метода**==, объявленного в текущем классе или унаследованного от суперклассов.  
	    Если метод с указанным именем и параметрами не найден, выбрасывается `NoSuchMethodException`.
	#### **Параметры:**
	1. **`name`**
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
	Класс `Calculator` содержит метод `add`, который принимает два параметра типа `int`.
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
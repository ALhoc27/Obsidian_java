- *Рефлексия*
	- *[[java.lang.reflect.Constructor]]*
	- *[[java.lang.reflect.Method]]*
	- *[[java.lang.reflect.Field]]*
	- *[[java.lang.reflect.Array]]*
	- *[[java.lang.reflect.Modifier]]*
	- *[[java.lang.reflect.Member]]*
	- *[[java.lang.reflect.Parameter]]*
	- *[[java.lang.reflect.ParameterizedType]]*

Класс `Class` — это часть Java Reflection API и основной инструмент для работы с метаинформацией о классах и объектах во время выполнения программы. Объекты этого класса представляют загруженные в JVM классы, интерфейсы, массивы и примитивные типы.

>[!NOTE] Title
> Метод **`getClass()`** в Java используется для получения объекта `Class`, представляющего класс текущего объекта. Это один из методов класса `Object`, поэтому доступен для любого объекта в Java.
>```java
>public final Class<?> getClass();
>```
> - **Возвращаемый тип:** `Class<?>` — объект класса `Class`, представляющий тип объекта, вызвавшего этот метод.
> - **Модификатор:** `final` — метод не может быть переопределен.

**Пример:** [^28]

---
#### **Как получить объект `Class`**
1. Через метод `getClass()` объекта
```java
String str = "Hello";
Class<?> clazz = str.getClass();
System.out.println(clazz.getName()); // java.lang.String
```
2.  Через `.class` литерал
```java
Class<String> clazz = String.class;
System.out.println(clazz.getName()); // java.lang.String
```
3. С помощью `Class.forName()` 
```java
try {
    Class<?> clazz = Class.forName("java.lang.String");
    System.out.println(clazz.getName()); // java.lang.String
} catch (ClassNotFoundException e) {
    e.printStackTrace();
}
```
4. Для примитивных типов
```java
Class<Integer> intClass = int.class;
System.out.println(intClass.getName()); // int
```
5. Для массивов
```java
int[] array = new int[10];
Class<?> clazz = array.getClass();
System.out.println(clazz.getName()); // [I (массив int)
```

### Описание основных методов с примерами

| **1. Получение информации о классе** |                                                                                                                                                            |
| ------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Имя класса                           | `String getName()`: Полное имя класса (включая пакет). [^22]                                                                                               |
|                                      | `String getSimpleName()`: Простое имя класса. [^1]                                                                                                         |
|                                      | `String getCanonicalName()`: Каноническое имя класса. [^2]                                                                                                 |
|                                      | `String getTypeName()`: Возвращает имя типа. Для классов и интерфейсов совпадает с `getCanonicalName()`.[^23]                                              |
| Пакет                                | `Package getPackage()`: Возвращает объект `Package` с информацией о пакете класса.                                                                         |
| **2. Проверка типа класса**          |                                                                                                                                                            |
| Тип класса                           | `boolean isInterface()`: Проверяет, является ли класс интерфейсом. [^3]                                                                                    |
|                                      | `boolean isEnum()`: Проверяет, является ли класс перечислением (enum). [^6]                                                                                |
|                                      | `boolean isAnnotation()`: Проверяет, является ли класс аннотацией. [^7]                                                                                    |
|                                      | `boolean isArray()`: Проверяет, является ли класс массивом. [^4]                                                                                           |
|                                      | `boolean isPrimitive()`: Проверяет, является ли класс примитивным типом. [^5]                                                                              |
|                                      | `boolean isSynthetic()`: Проверяет, является ли класс синтетическим (созданным компилятором). [^8]                                                         |
| **3. Работа с иерархией классов**    |                                                                                                                                                            |
|                                      | `Class<?> getSuperclass()` – Возвращает суперкласс текущего класса (или `null`, если суперкласса нет, например у `Object`). [^25]                          |
|                                      | `Class<?>[] getInterfaces()` – Возвращает массив интерфейсов, которые реализует класс. [^26]                                                               |
|                                      | `boolean isAssignableFrom(Class<?> cls)` – можно ли присвоить объект указанного класса переменной текущего типа. [^27]                                     |
| **4. Работа с методами**             | *[[java.lang.reflect.Method]]*                                                                                                                             |
|                                      | `Method[] getMethods()`: Возвращает публичные методы класса и его предков. [^9]                                                                            |
|                                      | `Method[] getDeclaredMethods()`: Возвращает все методы, объявленные в классе (включая `private`). [^10]                                                    |
|                                      | `Method getMethod(String name, Class<?>... parameterTypes)`: Возвращает публичный метод по имени и параметрам. [^11]                                       |
|                                      | `Method getDeclaredMethod(String name, Class<?>... parameterTypes)`: Возвращает объявленный метод. [^12]                                                   |
| **5. Работа с полями**               | *[[java.lang.reflect.Field]]*                                                                                                                              |
|                                      | `Field[] getFields()`: Возвращает массив всех публичных полей класса, включая унаследованные. [^13]                                                        |
|                                      | `Field[] getDeclaredFields()`: Возвращает массив всех полей, объявленных в классе (включая `private`). [^14]                                               |
|                                      | `Field getField(String name)`: Возвращает публичное поле по имени. [^15]                                                                                   |
|                                      | `Field getDeclaredField(String name)`: Возвращает объявленное поле по имени(включая `private`). [^16]                                                      |
| **6. Работа с конструкторами**       | *[[java.lang.reflect.Constructor]]*                                                                                                                        |
|                                      | `Constructor<?>[] getConstructors()`: Возвращает массив всех публичных конструкторов. [^17]                                                                |
|                                      | `Constructor<?>[] getDeclaredConstructors()`: Возвращает массив всех конструкторов, включая `private`. [^18]                                               |
|                                      | `Constructor<T> getConstructor(Class<?>... parameterTypes)`: Возвращает публичный конструктор с указанными параметрами. [^19]                              |
|                                      | `Constructor<T> getDeclaredConstructor(Class<?>... parameterTypes)`: Возвращает объявленный конструктор с указанными параметрами, включая `private`. [^20] |
| **7. Работа с аннотациями**          |                                                                                                                                                            |
|                                      | `<A extends Annotation> A getAnnotation(Class<A> annotationClass)` – аннотация определенного типа.                                                         |
|                                      | `Annotation[] getAnnotations()` – все аннотации, связанные с классом. [^29]                                                                                |
|                                      | `Annotation[] getDeclaredAnnotations()` – аннотации, объявленные в классе.                                                                                 |
| **8. Работа с вложенными классами**  |                                                                                                                                                            |
|                                      | `Class<?>[] getClasses()` – публичные вложенные классы и интерфейсы.                                                                                       |
|                                      | `Class<?>[] getDeclaredClasses()` – все вложенные классы и интерфейсы.                                                                                     |
|                                      | `Class<?> getDeclaringClass()` – внешний класс, если текущий класс является вложенным.                                                                     |
|                                      | `Class<?> getEnclosingClass()` – класс, в котором определен текущий.                                                                                       |
| **9. Работа с объектами**            |                                                                                                                                                            |
|                                      | `T newInstance()`: Создает объект, используя конструктор по умолчанию (**устарел**).                                                                       |
|                                      | `Constructor.newInstance()`: Рекомендуемый способ создания обьекта.                                                                                        |
| **10. Работа с массивами**           |                                                                                                                                                            |
|                                      | `Class<?> getComponentType()` – тип элементов массива (если класс представляет массив).                                                                    |
| **11. Проверка модификаторов**       |                                                                                                                                                            |
|                                      | `int getModifiers()` – возвращает модификаторы класса (например, `public`, `private`, `final`).                                                            |
|                                      | `boolean isAnnotationPresent(Class<? extends Annotation> annotationClass)` – проверяет наличие аннотации.                                                  |
#### **Рефлексия и безопасность**
При использовании класса `Class` и методов рефлексии необходимо учитывать:
1. **Доступ к приватным членам:**
    - Для работы с приватными полями и методами требуется вызов `setAccessible(true)`.
2. **Потеря типизации:**
    - Методы возвращают объекты `Class<?>`, что требует приведения типов.
3. **Снижение производительности:**
    - Рефлексия медленнее, чем прямой вызов методов или обращение к полям.




[^1]:Возвращает простое имя класса (без пакета).
	```java 
	System.out.println(ArrayList.class.getSimpleName()); // ArrayList
	```
[^2]: **Каноническое имя класса** — это полное имя класса, включающее его пакет и структурные особенности (например, вложенность). Оно отражает его "каноническое представление" в соответствии с Java Language Specification.
	
	Каноническое имя:
	1. **Содержит полный путь к классу**: пакет + имя класса.
	2. **Учитывает вложенность классов**: для вложенных классов используются точки (`.`).
	3. **Не определено для некоторых типов классов**: локальных и анонимных.
	
	```java
	Class<?> clazz = int[].class;
	System.out.println(clazz.getCanonicalName()); // int[]
	```

[^3]:Проверяет, является ли класс интерфейсом.
	```java
	System.out.println(Runnable.class.isInterface()); // true
	System.out.println(String.class.isInterface());  // false
	```

[^4]:Проверяет, является ли класс массивом.
	```java
	System.out.println(int[].class.isArray()); // true
	System.out.println(String.class.isArray()); // false
	```
[^5]:Проверяет, является ли класс примитивным типом (например, `int`, `double`).
	```java
	System.out.println(int.class.isPrimitive()); // true
	System.out.println(String.class.isPrimitive()); // false
	```
[^6]:Проверяет, является ли класс перечислением (`enum`).
	```java
	enum Day { MONDAY, TUESDAY }
	
	System.out.println(Day.class.isEnum()); // true
	System.out.println(String.class.isEnum()); // false
	```
[^7]:Проверяет, является ли класс аннотацией.
	```java
	@interface Example {}
	
	System.out.println(Example.class.isAnnotation()); // true
	```
[^8]:Проверяет, является ли класс синтетическим (созданным компилятором, например, для вложенных классов).
	```java
	class Outer {
	    class Inner {}
	}
	
	public class Main {
	    public static void main(String[] args) {
	        System.out.println(Outer.Inner.class.isSynthetic()); // false
	    }
	}
	```
[^9]:Возвращает массив всех публичных методов класса, включая унаследованные.
	```java
	import java.lang.reflect.Method;
	
	public class Main {
	    public static void main(String[] args) {
	        Class<?> clazz = String.class;
	
	        for (Method method : clazz.getMethods()) {
	            System.out.println(method.getName());
	        }
	    }
	}
	```
[^10]:Возвращает массив всех методов, объявленных в классе (включая `private`).
	```java
	class Example {
	    public void method1() {}
	    private void method2() {}
	}
	
	public class Main {
	    public static void main(String[] args) {
	        Class<?> clazz = Example.class;
	
	        for (Method method : clazz.getDeclaredMethods()) {
	            System.out.println(method.getName()); // method1, method2
	        }
	    }
	}
	```

[^11]:Возвращает публичный метод по имени и параметрам.
	```java
	Method method = String.class.getMethod("substring", int.class);
	System.out.println(method.getName()); // substring
	```

[^12]:Возвращает метод, объявленный в классе, по имени и параметрам.
	```java
	import java.lang.reflect.Method;
	
	class Example {
	    private void method(String name) {}
	}
	
	public class Main {
	    public static void main(String[] args) throws Exception {
	        Method method = Example.class.getDeclaredMethod("method", String.class);
	        System.out.println(method.getName()); // method
	    }
	}
	```

[^13]:Возвращает массив всех публичных полей класса, включая унаследованные.
	```java
	import java.lang.reflect.Field;
	
	class Example {
	    public int publicField;
	    private int privateField;
	}
	
	public class Main {
	    public static void main(String[] args) {
	        for (Field field : Example.class.getFields()) {
	            System.out.println(field.getName()); // publicField
	        }
	    }
	}
	```

[^14]:Возвращает массив всех полей, объявленных в классе (включая `private`).
	```java
	for (Field field : Example.class.getDeclaredFields()) {
	    System.out.println(field.getName()); // publicField, privateField
	}
	```
	

[^15]:Возвращает публичное поле по имени.
	```java
	Field field = Example.class.getField("publicField");
	System.out.println(field.getName()); // publicField
	```

[^16]:Возвращает поле, объявленное в классе, по имени.
	```java
	Field field = Example.class.getDeclaredField("privateField");
	System.out.println(field.getName()); // privateField
	```
[^17]:Возвращает массив всех публичных конструкторов.
	```java
	import java.lang.reflect.Constructor;
	
	class Example {
	    public Example() {}
	    private Example(String name) {}
	}
	
	public class Main {
	    public static void main(String[] args) {
	        for (Constructor<?> constructor : Example.class.getConstructors()) {
	            System.out.println(constructor);
	        }
	    }
	}
	```

[^18]:Возвращает массив всех конструкторов, включая `private`.
	```java
	for (Constructor<?> constructor : Example.class.getDeclaredConstructors()) {
	    System.out.println(constructor);
	}
	```

[^19]:Возвращает публичный конструктор с указанными параметрами.
	```java
	Constructor<?> constructor = Example.class.getConstructor();
	System.out.println(constructor);
	```

[^20]:Возвращает объявленный конструктор с указанными параметрами, включая `private`.
	```java
	Constructor<?> constructor = Example.class.getDeclaredConstructor(String.class);
	System.out.println(constructor);
	```

[^21]:Возвращает тип элементов массива.
	```java
	int[] array = new int[10];
	Class<?> clazz = array.getClass();
	System.out.println(clazz.getComponentType()); // int
	```

[^22]:Возвращает полное имя класса, включая имя пакета.
	```java
	Class<?> clazz = java.util.ArrayList.class;
	System.out.println(clazz.getName()); // java.util.ArrayList
	```

[^23]:Возвращает имя типа. Для классов и интерфейсов совпадает с `getCanonicalName()`.
	```java
	System.out.println(int[].class.getTypeName()); // int[]
	```

[^24]:Возвращает суперкласс текущего класса. Если суперкласса нет (например, у `Object`), возвращает `null`.
	```java
	System.out.println(ArrayList.class.getSuperclass()); // class java.util.AbstractList
	```

[^29]:Возвращает все аннотации, связанные с классом.
	```java
	Annotation[] annotations = Deprecated.class.getAnnotations();
	for (Annotation annotation : annotations) {
	    System.out.println(annotation.toString());
	}
	```

[^25]:Возвращает суперкласс текущего класса. Если суперкласса нет (например, у `Object`), возвращает `null`.
	```java
	System.out.println(ArrayList.class.getSuperclass()); // class java.util.AbstractList
	```

[^26]:Возвращает массив интерфейсов, которые реализует класс.
	```java
	Class<?>[] interfaces = ArrayList.class.getInterfaces();
	for (Class<?> i : interfaces) {
	    System.out.println(i.getName());
	}
	// java.util.List
	// java.util.RandomAccess
	// java.lang.Cloneable
	// java.io.Serializable
	```

[^27]:Проверяет, можно ли присвоить объект указанного класса переменной текущего типа.
	```java
	System.out.println(List.class.isAssignableFrom(ArrayList.class)); // true
	```

[^28]:#### **Пример использования**
	##### **1. Базовое использование**
	```java
	class Example {}
	
	public class Main {
	    public static void main(String[] args) {
	        Example example = new Example();
	        Class<?> clazz = example.getClass();
	        System.out.println("Class name: " + clazz.getName()); // Class name: Example
	    }
	}
	```
	##### **2. Сравнение объектов**
	```java
	class Parent {}
	class Child extends Parent {}
	
	public class Main {
	    public static void main(String[] args) {
	        Parent parent = new Parent();
	        Parent child = new Child();
	
	        System.out.println("Parent class: " + parent.getClass()); // Parent class: class Parent
	        System.out.println("Child class: " + child.getClass()); // Child class: class Child
	
	        // Сравнение классов
	        System.out.println(parent.getClass() == child.getClass()); // false
	    }
	}
	```
	##### **3. Отличие от оператора `instanceo**f`
	Метод `getClass()` проверяет точный класс объекта, тогда как `instanceof` проверяет, является ли объект экземпляром данного класса или ==его подклассов==.
	```java
	class Parent {}
	class Child extends Parent {}
	
	public class Main {
	    public static void main(String[] args) {
	        Parent child = new Child();
	
	        System.out.println("Using getClass(): " + (child.getClass() == Parent.class)); // Using getClass(): false
	        System.out.println("Using instanceof: " + (child instanceof Parent)); // Using instanceof: true
	    }
	}
	```
	##### 4. Рефлексия
	`getClass()` используется для получения метаданных класса, например:
	- Методы класса (`getMethods()`)
	- Конструкторы (`getConstructors()`)
	- Поля (`getFields()`)
	```java
	public class Main {
	    public static void main(String[] args) {
	        String str = "Hello";
	        Class<?> clazz = str.getClass();
	
	        System.out.println("Methods:");
	        for (var method : clazz.getMethods()) {
	            System.out.println(method.getName());
	        }
	    }
	}
	```
	

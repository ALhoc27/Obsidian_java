##### **1. Получение информации о классе**
###### - **Имя класса**
- `String getName()`: Полное имя класса (включая пакет).
- `String getSimpleName()`: Простое имя класса. [^1]
- `String getCanonicalName()`: Каноническое имя класса.
```java
Class<?> clazz = String.class;
System.out.println(clazz.getName());         // java.lang.String
System.out.println(clazz.getSimpleName());   // String
System.out.println(clazz.getCanonicalName());// java.lang.String
```
###### - **Пакет**
- `Package getPackage()`: Возвращает объект `Package` с информацией о пакете класса.
```java
Class<?> clazz = String.class;
Package pkg = clazz.getPackage();
System.out.println(pkg.getName()); // java.lang
```

##### **2. Проверка типа класса**
###### - **Тип класса**
- `boolean isInterface()`: Проверяет, является ли класс интерфейсом.
- `boolean isEnum()`: Проверяет, является ли класс перечислением (enum).
- `boolean isAnnotation()`: Проверяет, является ли класс аннотацией.
- `boolean isArray()`: Проверяет, является ли класс массивом.
- `boolean isPrimitive()`: Проверяет, является ли класс примитивным типом.
- `boolean isSynthetic()`: Проверяет, является ли класс синтетическим (созданным компилятором).
```java
System.out.println(String.class.isInterface()); // false
System.out.println(int.class.isPrimitive());    // true
System.out.println(int[].class.isArray());      // true
```

##### **3. Работа с иерархией классов**
###### - **Родительский класс**
- `Class<?> getSuperclass()`: Возвращает суперкласс текущего класса (или `null`, если суперкласса нет, например у `Object`).
```java
Class<?> clazz = Integer.class;
System.out.println(clazz.getSuperclass().getName()); // java.lang.Number
```
###### - **Реализованные интерфейсы**
- `Class<?>[] getInterfaces()`: Возвращает массив интерфейсов, которые реализует класс.
```java
Class<?> clazz = ArrayList.class;
for (Class<?> iface : clazz.getInterfaces()) {
    System.out.println(iface.getName()); // java.util.List, java.util.RandomAccess и т.д.
}
```

##### **4. Работа с методами, полями и конструкторами**
###### - **Получение методов**
- `Method[] getMethods()`: Возвращает публичные методы класса и его предков.
- `Method[] getDeclaredMethods()`: Возвращает все методы, объявленные в классе (включая `private`).
- `Method getMethod(String name, Class<?>... parameterTypes)`: Возвращает метод по имени и параметрам.
- `Method getDeclaredMethod(String name, Class<?>... parameterTypes)`: Возвращает объявленный метод.
```java
import java.lang.reflect.Method;

class Example {
	public void method1() {}
	private void method2() {}
}

public class Main {
	public static void main(String[] args) {
		Class<?> clazz = Example.class;
		for (Method method : clazz.getDeclaredMethods()) {
			System.out.println(method.getName());
		}
	}
}
```
###### - **Получение полей**
- `Field[] getFields()`: Возвращает публичные поля класса.
- `Field[] getDeclaredFields()`: Возвращает все поля, объявленные в классе.
- `Field getField(String name)`: Возвращает публичное поле.
- `Field getDeclaredField(String name)`: Возвращает объявленное поле.
```java
import java.lang.reflect.Field;

class Example {
    public int publicField;
    private int privateField;
}

public class Main {
    public static void main(String[] args) {
        Class<?> clazz = Example.class;
        for (Field field : clazz.getDeclaredFields()) {
            System.out.println(field.getName());
        }
    }
}
```
###### - **Получение конструкторов**
- `Constructor<?>[] getConstructors()`: Возвращает публичные конструкторы.
- `Constructor<?>[] getDeclaredConstructors()`: Возвращает все конструкторы.
- `Constructor<T> getConstructor(Class<?>... parameterTypes)`: Возвращает публичный конструктор.
- `Constructor<T> getDeclaredConstructor(Class<?>... parameterTypes)`: Возвращает объявленный конструктор.
```java
import java.lang.reflect.Constructor;

class Example {
    public Example() {}
    private Example(String name) {}
}

public class Main {
    public static void main(String[] args) {
        Class<?> clazz = Example.class;
        for (Constructor<?> constructor : clazz.getDeclaredConstructors()) {
            System.out.println(constructor);
        }
    }
}
```

##### **5. Работа с массивами**
###### - **Тип элементов массива**
- `Class<?> getComponentType()`: Возвращает тип элементов массива.
```java
int[] array = new int[10];
Class<?> clazz = array.getClass();
System.out.println(clazz.getComponentType()); // int
```

##### **6. Создание объектов**
###### - **Создание экземпляра**
- `T newInstance()`: Создает объект, используя конструктор по умолчанию (**устарел**).
- `Constructor.newInstance()`: Рекомендуемый способ.
```java
class Example {
    public Example() {
        System.out.println("Объект создан");
    }
}

public class Main {
    public static void main(String[] args) throws Exception {
        Class<?> clazz = Example.class;
        Object instance = clazz.getDeclaredConstructor().newInstance();
    }
}
```

#### **Рефлексия и безопасность**

При использовании класса `Class` и методов рефлексии необходимо учитывать:
1. **Доступ к приватным членам:**
    - Для работы с приватными полями и методами требуется вызов `setAccessible(true)`.
2. **Потеря типизации:**
    - Методы возвращают объекты `Class<?>`, что требует приведения типов.
3. **Снижение производительности:**
    - Рефлексия медленнее, чем прямой вызов методов или обращение к полям.
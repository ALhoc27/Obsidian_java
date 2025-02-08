Метод **`getMethods()`** принадлежит классу **`Class`** ([[java.lang.Class<T>]]) и предназначен для получения всех **публичных методов** текущего класса и его суперклассов, включая методы, унаследованные от класса `Object`.
```java
public Method[] getMethods() throws SecurityException
```
**Описание:** Возвращает массив 🟤 всех **публичных методов**, объявленных в текущем классе и унаследованных от суперклассов.  
	Это включает методы из класса `Object` (`toString()`, `equals()`, `hashCode()` и др.)
**Особенности:**
	- Возвращает только методы, объявленные как `public`.
	- Поддерживает методы суперклассов.
	- Полезно для перечисления всех доступных публичных методов.

**Пример:**
```java
import java.lang.reflect.Method;

class Example {
	public void publicMethod() {}
	private void privateMethod() {}
}

public class Main {
	public static void main(String[] args) {
🟤      Method[] methods = Example.class.getMethods();

		for (Method method : methods) {
			System.out.println("Метод: " + method.getName());
		}
	}
}
```
**Результат:**
```yaml
Метод: publicMethod
Метод: equals
Метод: toString
Метод: hashCode
Метод: getClass
Метод: notify
Метод: notifyAll
Метод: wait
Метод: wait
Метод: wait
```
[[Разобрать результат№1]]
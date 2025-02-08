- *[[boolean equals(Object obj)]]*

**==Метод `equals()` определяет, равны ли два объекта логически (смыслово)==.**
Контракт метода `equals()` в Java описывает, как метод должен быть реализован, чтобы обеспечить ожидаемое поведение при сравнении объектов. Этот контракт состоит из следующих правил:

1. **[[Рефлексивность (Reflexivity)]]:**
    Для любого объекта `x`, вызов `x.equals(x)` должен возвращать `true`. 
2. **[[Симметричность (Symmetry)]]:**
    Для любых объектов `x` и `y`, если `x.equals(y)` возвращает `true`, то и `y.equals(x)` также должен вернуть `true`.  [[Симметричность (Symmetry)]]
3. **[[Транзитивность (Transitivity)]]:**
    Для любых объектов `x`, `y` и `z`, если `x.equals(y)` возвращает `true` и `y.equals(z)` возвращает `true`, то и `x.equals(z)` должен возвращать `true`.
4. **[[Согласованность (Consistency)]]:**
    Для любых объектов `x` и `y`, многократные вызовы `x.equals(y)` должны возвращать одно и то же значение, пока объекты остаются неизменными (не изменяются их значимые поля).
5. **[[Сравнение с null в контексте equals()]]:**
    Для любого объекта `x`, вызов `x.equals(null)` должен возвращать `false`.

#### Типичная реализация метода equals()
Реализация метода `equals()` часто предполагает сравнение значимых полей объекта. Вот пример:
```java
@Override
public boolean equals(Object obj) {
    if (this == obj) return true; // Рефлексивность
    if (obj == null || getClass() != obj.getClass()) return false; // Проверка на null и одинаковый класс
    MyClass other = (MyClass) obj; // Приведение типов
    return Objects.equals(field1, other.field1) && Objects.equals(field2, other.field2); // Сравнение значимых полей
}
```

#### Рекомендации
1. **Переопределяйте `hashCode()` вместе с `equals()`.**  
    Это важно для корректной работы объектов в коллекциях, например, в `HashMap` или `HashSet`.
    
2. **Используйте `Objects.equals()`.**  
    Это упрощает сравнение полей и предотвращает возможные ошибки, связанные с `NullPointerException`.
    
3. **Сравнивайте только значимые поля.**  
    Учитывайте только те поля, которые имеют смысл для логического равенства объектов.

#### Пример использования
Если вы сравниваете два объекта, например, `Person`, где важны только `name` и `age`:
```java
public class Person {
    private String name;
    private int age;

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Person person = (Person) obj;
        return age == person.age && Objects.equals(name, person.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }
}Метод `equals()` определяет, равны ли два объекта логически (смыслово). Контракт этого метода гарантирует, что он ведет себя предсказуемо и корректно. Он включает следующие ключевые требования:

```


В Java метод `Objects.equals()` используется для удобного и безопасного сравнения объектов, особенно если один из них может быть `null`. Рассмотрим оба варианта сравнения и их различия.
<table class="language-java_td" style="width: 99%; border-collapse: collapse; margin-bottom: 5px;">
	<tr>
		<strong style="font-size: 1.1em; color: #333;">Пример :</strong>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333; line-height: 1.5;"><span style="border: 1px solid black; padding: 2px;">#1</span>
&nbsp; Сравнение без <code>Objects.equals()</code></strong><br/>
Если вы используете стандартный метод <code>equals()</code>, необходимо учитывать ситуацию с <code>null</code> вручную:
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd; background-color: #f2efed">
            <strong style="font-size: 1em; color: #333; line-height: 1.5;"><span style="border: 1px solid black; padding: 2px;">#2</span>
&nbsp; Сравнение с <code>Objects.equals()</code><br/></strong>
С <code>Objects.equals()</code> код становится проще и безопаснее:
        </td>
    </tr>
    <tr>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre class="language-java_td" style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
class Person {
    private String name;
 
    public Person(String name) {
        this.name = name;
    }
 
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true; // Сравнение ссылок
        if (obj == null || getClass() != obj.getClass()) return false; // Проверка на null и класс
        Person other = (Person) obj;
🔴		return name != null ? name.equals(other.name) : other.name == null; // Проверка на null вручную
    }
 
    @Override
    public int hashCode() {
        return name != null ? name.hashCode() : 0;
    }
}
				</code>
            </pre>
        </td>
        <td style="padding: 5px 10px; border: 1px solid #ddd;">
            <pre style="background-color: #f4f4f4; color: #f8f8f8; margin: 0px; padding: 0px 10px; border-radius: 5px; font-size: 0.9em; overflow-x: auto;">
				<code class="language-java language-java_td" style="font-family: 'Courier New', monospace; padding: 0px; margin: 0px;">
import java.util.Objects;
 
class Person {
    private String name;
 
    public Person(String name) {
        this.name = name;
    }
 
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true; // Сравнение ссылок
        if (obj == null || getClass() != obj.getClass()) return false; // Проверка на null и класс
        Person other = (Person) obj;
🔵		return Objects.equals(name, other.name); // Автоматическая обработка null
    }
 
    @Override
    public int hashCode() {
        return Objects.hash(name);
    }
}
				</code>
            </pre>
        </td>
    </tr>
</table>

###### Подробнее <span style="border: 1px solid black; padding: 2px; line-height: 1.75;">#1</span>: &nbsp; <br/>
Обычно сравнение выполняется с явной проверкой `null`, чтобы избежать `NullPointerException`:&nbsp;&nbsp;&nbsp;<dir style="
    width: 100%; 
    border-collapse: collapse; 
    font-family: Arial, sans-serif; 
    font-size: 15px; 
    text-align: left; 
    margin: 0px 5px; 
    padding: 5px 5px; 
    background-color: rgba(255, 165, 0, 0.3);
    border-radius: 8px; 
    overflow: hidden; 
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
	border: 1px solid #d6d8db;
"> &nbsp;&nbsp;<b>Недостатки:</b>
	<li> Приходится вручную проверять `null`, что делает код более громоздким.
	<li> Повышается вероятность ошибки, если забыть проверить `null`.
</dir>

###### Подробнее <span style="border: 1px solid black; padding: 2px; line-height: 1.75;">#2</span>: &nbsp; <br/>
Метод `Objects.equals()` используется для удобного и безопасного сравнения объектов, особенно если один из них может быть `null`, делает код более лаконичным:<dir style="
    width: 100%; 
    border-collapse: collapse; 
    font-family: Arial, sans-serif; 
    font-size: 15px; 
    text-align: left; 
    margin: 0px 5px; 
    padding: 5px 5px; 
    background-color: rgba(255, 165, 0, 0.3);
    border-radius: 8px; 
    overflow: hidden; 
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
	border: 1px solid #d6d8db;
"> &nbsp;&nbsp;<b>Преимущества:</b>
	<li>Безопасность: `Objects.equals(a, b)` сам проверяет `null`, не вызывая `NullPointerException`.
	<li>Читаемость: код становится более чистым и кратким.
	<li>Универсальность: можно легко заменить сравнение нескольких поле
</dir>

### **Вывод**
Использование `Objects.equals()` упрощает код, устраняет необходимость ручной проверки `null` и делает `equals()` более надежным и читаемым.

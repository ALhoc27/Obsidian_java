`super.equals(obj)` - ==**означает вызов метода `equals()` из суперкласса текущего объекта**== (в данном случае, из класса, от которого наследуется текущий класс). Это позволяет использовать реализацию метода `equals()` в суперклассе для сравнения тех полей, которые определены в этом суперклассе.

Использование `super.equals()` в методе `equals()` класса `ExtendedPerson` имеет важное значение для правильного сравнения объектов, особенно в ситуации, когда класс `ExtendedPerson` является подклассом `Person`. 
Вызов `super.equals()` позволяет выполнить сравнение полей, определённых в суперклассе (`Person`), перед тем как добавлять сравнение дополнительных полей (`age`) в подклассе (`ExtendedPerson`). Это упрощает логику и помогает избежать дублирования кода, который уже реализован в `equals()` суперкласса.
### **Контекст вызова `super.equals(obj)`**
Когда вы переопределяете метод `equals()` в подклассе, вам нужно учитывать поля как из суперкласса, так и из подкласса. Вместо того, чтобы повторно реализовывать логику сравнения полей суперкласса, вы вызываете `super.equals(obj)`.

Этот вызов:
1. Сравнивает те поля, которые определены в суперклассе.
2. Возвращает результат (`true` или `false`) в зависимости от того, равны ли поля суперкласса.

**Пример:**
```java
class Person {
	private String name;

	public Person(String name) {
		this.name = name;
	}

	@Override
	public boolean equals(Object obj) {
		if (this == obj) return true; // Проверка на совпадение ссылок
		if (obj == null || getClass() != obj.getClass()) return false; // Типы объектов не совпадают
		Person other = (Person) obj;
		return name.equals(other.name); // Сравнение поля name
	}
}

class ExtendedPerson extends Person {
	private int age;

	public ExtendedPerson(String name, int age) {
		super(name);
		this.age = age;
	}

	@Override
	public boolean equals(Object obj) {
		if (this == obj) return true;
		if (obj == null || getClass() != obj.getClass()) return false;

		// Сравнение полей суперкласса через super.equals()
		if (!super.equals(obj)) return false;

		// Сравнение полей подкласса
		ExtendedPerson other = (ExtendedPerson) obj;
		return this.age == other.age;
	}
}
```
#### **Что происходит при вызове `super.equals(obj)`?**
1. Если объект `obj` передан в метод `equals()` класса `ExtendedPerson`, сначала будет вызван метод `equals()` из `Person` через `super.equals(obj)`.
2. Внутри `super.equals(obj)` происходит сравнение поля `name` между текущим объектом (`this`) и объектом `obj`.
3. Если поля суперкласса равны, метод возвращает `true`, и выполнение продолжается для сравнения полей подкласса.
4. Если поля суперкласса не равны, метод возвращает `false`, и дальнейшее сравнение прекращается.

#### То есть:
 1. **После проверок:**
```java
if (this == obj) return true;
if (obj == null || getClass() != obj.getClass()) return false;
```
- Проверка на "самого себя" `this == obj` - та же самая ссылка(*тот же обьект или нет*)
- `if (obj == null || getClass() != obj.getClass())` - необходима проверка на `null` (*так как метод `getClass()`, небезопасен для `null`, при `null` выбрасывается исключение `NullPointerException`*)
2. **Прежде выполнится(будет вызван) метод супер класса:**
```java
// Сравнение полей суперкласса через super.equals()
if (!super.equals(obj)) return false;
```
Метод супер класса (класса родитель `Person`):
```java
@Override
public boolean equals(Object obj) {
	if (this == obj) return true; // Проверка на совпадение ссылок
	if (obj == null || getClass() != obj.getClass()) return false; // проверкау на принадлежность одному и тому же классу, с проверкой на null
	Person other = (Person) obj;
	return name.equals(other.name); // Сравнение поля name
}
```
Так как класс `Person`, класс родитель класса `ExtendedPerson` то без проблем `Person other = (Person) obj;` (проводится каст), и сравниваются поля, возвращая `true` / `false`

> [!NOTE] Важно:
>  `!super.equals(obj)` - вызов метода `equals()` из суперкласса ==**текущего объекта**== (то есть данный метод супер класса вызывается на текущем обьекте)
>```java
>public static void main(String[] args) {  
>   ExtendedPerson extendedPerson = new ExtendedPerson("sasa", 12);  
>   ExtendedPerson extendedPerson1 = new ExtendedPerson("sasa", 12);  
>   System.out.println(extendedPerson.equals(extendedPerson1));  
>}
>```
>Текущий обьект (пример выше), у нас `extendedPerson`, у него и вызывается метод `equals()` из суперкласса

3. После сравнения полей супер класса, сравниваются поля на уровне под класса:
```java
// Сравнение полей подкласса
ExtendedPerson other = (ExtendedPerson) obj;
return this.age == other.age;
```


> [!TRIP] Важно помнить:
>```java
if (obj == null || getClass() != obj.getClass()) return false; // Типы объектов не совпадают
>```
> Что `getClass()` - не привязан какому то конкретному классу, этот метод возвращает класс текущего объекта (на котором вызывается данный метод).
> **Выражение:**
>```java
>getClass() != obj.getClass()
>```
>Означает жесткую проверку, того что класс текущего обьекта равен классу `obj` (*обьект переданный аргументом методу `equals(obj)`*)
>Так же `getClass()` **не безопасен для `null`** (в случае есть обьект `null` выбросится исключение `NullPointerException`), по этому необходима проверка на `null` [^1]
>
> В свою очередь `instanceof` - используется для проверки, является ли объект экземпляром определённого класса или подкласса. (**в том числе для наследников**, проверка не жесткая)


<br/><div style="text-align: center; margin: 0; padding: 0;"> <span style="color: #ff7e5f; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> <span style="color: #feb47b; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> <span style="color: #4facfe; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> </div>

[^1]:![[Снимок экрана 2025-01-24 в 16.11.49.png]]
	![[Снимок экрана 2025-01-24 в 16.14.46.png|550]]
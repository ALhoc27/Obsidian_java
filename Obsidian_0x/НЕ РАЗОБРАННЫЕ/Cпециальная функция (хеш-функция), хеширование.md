Специальная функция, которая преобразует объект в число (хеш), называется **хеш-функцией**.  
В Java роль хеш-функции выполняет метод `hashCode()`, который можно переопределить для своих объектов.
#### **Как работает хеш-функция?**
Хеш-функция берёт данные объекта и вычисляет для него число (**хеш-код**).  
*Например:*
```java
"Apple"  → 123456  
"Banana" → 987654  
"Orange" → 456789  
```
Это просто пример чисел. В реальности Java использует сложные алгоритмы.

#### **Какие хеш-функции есть в Java?**
##### **1. Стандартная `hashCode()` из `Object`**
Каждый объект в Java по умолчанию имеет `hashCode()`, но он обычно основан на адресе в памяти.
```java
Object obj = new Object();
System.out.println(obj.hashCode()); // Например, 1829164700
```
Это не очень полезно для наших классов, потому что одинаковые объекты могут получить разные хеши. 

##### 2. `String.hashCode()` - Java уже переопределяет `hashCode()` для строк.

<div class="cm-line1">
<span class="cm-line" style="margin: 0; line-height: 1.2; display: inline-block; font-size: 16px;
    font-weight: bold;
    color: #1E587F;
    text-decoration: underline;
    text-decoration-color: transparent;
    text-decoration-thickness: 3px;
    background: linear-gradient(to right, #E4C257, transparent);
    background-size: 100% 3px;
    background-repeat: no-repeat;
    background-position: bottom;
    padding-bottom: 5px;"> &nbsp;&nbsp;Разберём пошагово, как работает переопределённый метод `hashCode()` для класса `String` в Java. Вот </span></div>

| <span style="font-size: 1.04em; font-weight: bold; margin: 0; line-height: 1.2; display: inline-block; margin-bottom: 10px; "> &nbsp;&nbsp; Переопределённый метод `hashCode()` для класса `String`: </span>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | <span style="font-size: 1.04em; font-weight: bold; margin: 0; line-height: 1.2; display: inline-block; margin-bottom: 10px;"> &nbsp;&nbsp; Заголовок: </span>                                      |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| - **==Вносить построчно==**<br>Можно выделить более компактно (⠀), с двумя пробелами, но и стандартное форматирование так же поддерживается<br>**Поставь в коде обычный пробел где пустая строка**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | - **==Вносить построчно==**<br>Можно выделить более компактно (⠀), с двумя пробелами, но и стандартное форматирование так же поддерживается<br>**Поставь в коде обычный пробел где пустая строка** |
| <div class="code_md_tab"><br><code class="language-java language-java_td specific-override"><br>public int hashCode() {<br></code><br><code class="language-java language-java_td specific-override"><br>    int h = 0;<br></code><br><code class="language-java language-java_td specific-override"><br>    for (char c : this.toCharArray()) {<br></code><br><code class="language-java language-java_td specific-override"><br>        h = 31 * h + c;<br></code><br><code class="language-java language-java_td specific-override"><br>    }<br></code><br><code class="language-java language-java_td specific-override"><br>    return h;<br></code><br><code class="language-java language-java_td specific-override"><br>}<br></code>⠀⠀⠀⠀<br></div> |                                                                                                                                                                                                    |
| Выделить строку можно - 🟤 🟣 🟠 🔵 🔴   <br>Для того что бы выравнять колонки, добавьте на след строке данный пробел (⠀)<br>или попробуйте убрать `display: inline-block; margin-bottom: 10px;`)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Выделить строку можно - 🟤 🟣 🟠 🔵 🔴   <br>Для того что бы выравнять колонки, добавьте на след строке данный пробел (⠀)<br>или попробуйте убрать `display: inline-block; margin-bottom: 10px;`)  |




Вот как это работает:
```java
public int hashCode() {
    int h = 0;
    for (char c : this.toCharArray()) {
        h = 31 * h + c;
    }
    return h;
}
```














<br/><div style="text-align: center; margin: 0; padding: 0;"> <span style="color: #ff7e5f; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> <span style="color: #feb47b; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> <span style="color: #4facfe; font-size: 20px; display: inline; margin: 10; padding: 0;"> ● </span> </div>

[^1]:

[^2]:

[^3]:

[^4]:

[^5]:

[^6]:

[^7]:

[^8]:

[^9]:

[^10]:

[^11]:

[^12]:

[^13]:

[^14]:

[^15]:

[^16]:

[^17]:

[^18]:

[^19]:

[^20]:



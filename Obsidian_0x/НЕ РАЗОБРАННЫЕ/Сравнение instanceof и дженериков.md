#### **1. `instanceof`**
- **Когда использовать:**
    - Когда тип объекта неизвестен во время компиляции.
    - Когда код работает с объектами, возвращаемыми из старых API, не использующих дженерики.
    - В случаях, когда нужно проверить, относится ли объект к определенному типу, не используя параметризацию.

- **Плюсы:**
    - Универсальность: работает со всеми объектами, независимо от их типа.
    - Подходит для смешанных данных, где заранее неизвестен тип объекта.

- **Минусы:**
    - Требуется явное приведение типов, что может привести к ошибкам времени выполнения (`ClassCastException`), если неправильно использовать.
    - Меньше безопасности типов, чем у дженериков.

**Пример:**
```java
Object obj = "Hello";

if (obj instanceof String) {
    String str = (String) obj; // Безопасное приведение
    System.out.println(str.toUpperCase());
}
```


| 1. <span style="font-size: 1.3em; font-weight: bold; margin: 0; line-height: 1.2; display: inline-block; margin-bottom: 10px;"> `instanceof`</span><br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | 2. <span style="font-size: 1.2em; font-weight: bold; margin: 0; line-height: 1.2; display: inline-block; margin-bottom: 10px;"> Дженерики</span><br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| - **Когда использовать:**<br>    - Когда тип объекта неизвестен во время компиляции.<br>    - Когда код работает с объектами, возвращаемыми из старых API, не использующих дженерики.<br>    - В случаях, когда нужно проверить, относится ли объект к определенному типу, не используя параметризацию.<br><br>- **Плюсы:**<br>    - Универсальность: работает со всеми объектами, независимо от их типа.<br>    - Подходит для смешанных данных, где заранее неизвестен тип объекта.<br><br>- **Минусы:**<br>    - Требуется явное приведение типов, что может привести к ошибкам времени выполнения (`ClassCastException`), если неправильно использовать.<br>    - Меньше безопасности типов, чем у дженериков.<br><br>**Пример:** | **Когда использовать:**<br>    - Когда тип объекта известен во время компиляции.<br>    - Для коллекций и других структур данных, работающих с объектами одного типа.<br>    - Чтобы избежать явного приведения типов.<br><br>- **Плюсы:**    <br>    - Типобезопасность: ошибки обнаруживаются на этапе компиляции.<br>    - Нет необходимости в явном приведении типов, что упрощает код.<br>    - Читаемость: код становится понятнее, так как типы данных определены явно.<br><br>- **Минусы:**    <br>    - Дженерики работают только с объектами (нет поддержки примитивов напрямую, но можно использовать их обертки, например, `Integer` для `int`).<br>    - Иногда может быть избыточным для задач, где тип заранее неизвестен.<br><br>**Пример:** |

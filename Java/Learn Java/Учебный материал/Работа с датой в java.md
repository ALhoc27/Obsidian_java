В Java работа с датой и временем разделена на **старые классы** и **новые API**.
### **Старые классы (до Java 8):**
Эти классы изменяемы и имеют множество недостатков:
1. **`Date`**:
    - Изменяемый.
    - Устарел (deprecated для многих операций).
    - Хранит время в миллисекундах с 1 января 1970 года.
    - Методы для изменения (`setTime`, `setYear` и т.д.).
```java
Date date = new Date();
date.setTime(1000000L); // Изменение времени
```
    
2. **`Calendar`**:
    - Изменяемый.
    - Позволяет изменять поля, такие как год, месяц, день.
```java
Calendar cal = Calendar.getInstance();
cal.set(Calendar.YEAR, 2025); // Изменение года
```
    
3. **`SimpleDateFormat`**:
    - Изменяемый.
    - Используется для форматирования дат.
```java
SimpleDateFormat sdf = new SimpleDateFormat("dd/MM/yyyy");
sdf.applyPattern("MM-dd-yyyy"); // Изменение формата
```

#### **Недостатки старых классов:**
- Изменяемость делает их непотокобезопасными.
- Сложность работы с датой (например, индексация месяцев начинается с 0).
- Ограниченные функциональные возможности.
---

### **Новые API для даты и времени (Java 8+):**

В Java 8 представили новый пакет `java.time`, который предлагает классы для работы с датой и временем. Эти классы:
- Основаны на библиотеке Joda-Time.
- **Неизменяемые** и потокобезопасные.
- Обеспечивают удобную и современную работу с датой, временем и их форматированием.
---
#### **Основные классы нового API**
1. **`LocalDate`** (Только дата):
    - Неизменяемый.
    - Представляет дату без времени.
```java
LocalDate date = LocalDate.now();
LocalDate newDate = date.plusDays(5); // Создан новый объект
```
    
2. **`LocalTime`** (Только время):
    - Неизменяемый.
    - Представляет время без даты.
```java
LocalTime time = LocalTime.now();
LocalTime newTime = time.plusHours(2); // Создан новый объект
```
    
3. **`LocalDateTime`** (Дата и время):
    - Неизменяемый.
    - Содержит дату и время, но без информации о часовом поясе.
```java
LocalDateTime dateTime = LocalDateTime.now();
LocalDateTime newDateTime = dateTime.plusMonths(1); // Создан новый объект
```
    
4. **`ZonedDateTime`** (Дата и время с часовым поясом):
    - Неизменяемый.
    - Используется для работы с часовыми поясами.
```java
ZonedDateTime zdt = ZonedDateTime.now();
ZonedDateTime newZdt = zdt.plusHours(3); // Создан новый объект
```
    
5. **`Instant`**:
    - Неизменяемый.
    - Представляет точное мгновение во времени (в наносекундах с эпохи 1970-01-01T00:00:00Z).
```java
Instant instant = Instant.now();
Instant newInstant = instant.plusSeconds(3600); // Создан новый объект
```

---

#### **Изменяемы ли новые классы?**
- **Нет, новые классы неизменяемые.**  
    Любая операция (например, добавление дней, времени) создаёт новый объект, не изменяя исходный.

*Пример:*
```java
LocalDate date = LocalDate.now();
LocalDate updatedDate = date.plusDays(10); // Исходная дата остаётся неизменной

System.out.println(date);         // Исходная дата
System.out.println(updatedDate);  // Новая дата
```

---

#### **Преимущества новых классов:**

1. **Неизменяемость**:
    - Гарантирует потокобезопасность.
    - Исключает случайные изменения объекта.

1. **Удобство использования**:    
    - Читаемые методы: `plusDays`, `minusMonths`, `withYear`.
    - Поддержка форматирования с помощью `DateTimeFormatter`.
```java
LocalDate date = LocalDate.now();
String formattedDate = date.format(DateTimeFormatter.ofPattern("dd/MM/yyyy"));
```
    
3. **Работа с часовыми поясами**:
    - Использование классов `ZoneId` и `ZonedDateTime` для точной работы с временными зонами.
```java
ZonedDateTime zdt = ZonedDateTime.now(ZoneId.of("America/New_York"));
```
    
4. **Богатый функционал**:
    - Удобные методы для вычислений (разницы между датами, добавление интервалов и т.д.).

---

### **Сравнение старых и новых классов**

| **Характеристика**     | **Старые классы**      | **Новые классы**      |
| ---------------------- | ---------------------- | --------------------- |
| **Изменяемость**       | Изменяемые             | Неизменяемые          |
| **Потокобезопасность** | Нет                    | Да                    |
| **Часовые пояса**      | Ограниченная поддержка | Полноценная поддержка |
| **Удобство API**       | Сложное                | Простое               |
| **Функционал**         | Ограниченный           | Широкий               |

---

### **Вывод**
- Используйте новые классы из пакета `java.time` вместо устаревших (`Date` и `Calendar`).
- Новые классы неизменяемы, что упрощает их использование в многопоточных приложениях.
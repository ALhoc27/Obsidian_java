Garbage Collection (GC) — это автоматический процесс управления памятью, осуществляемый JVM. Его цель — освобождение памяти, занятой объектами, которые больше не используются в программе.

|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <span style="font-size: 1.2em; font-weight: bold; margin: 0; line-height: 1.2; display: inline-block; margin-bottom: 10px;"> &nbsp;&nbsp;Сборщик мусора</span><br>Сборщик мусора (Garbage Collector, GC) — это процесс в виртуальной машине Java (JVM), который автоматически освобождает память, выделенную для объектов, которые больше не используются. Этот процесс происходит следующим образом:<br><br>- **Маркировка**: Сборщик мусора начинает “маркировать” все объекты в куче, которые больше не доступны из корней приложения. “Корни” обычно включают в себя стек вызова и глобальные ссылки. Если на объект в куче не существует активной ссылки из этих “корней”, он считается недоступным.<br>- **Удаление**: После того как недоступные объекты были помечены, сборщик мусора освобождает память, которую они занимали.<br><br>Несмотря на автоматизацию управления памятью, неэффективное использование ресурсов может по-прежнему привести к проблемам. Например, ==если приложение постоянно создаёт новые объекты и сохраняет на них ссылки, это может привести к утечке памяти==, когда куча постепенно заполняется, и система больше не может выделить память для новых объектов. В таких случаях приложение может завершиться с ошибкой `OutOfMemoryError`. |

### 1. **Зачем нужна сборка мусора?**
- Устраняет необходимость ручного управления памятью, как в языках вроде C/C++.
- Предотвращает утечки памяти.
- Оптимизирует использование оперативной памяти приложения. (очищает память от уже не нужных объектов)
### 2. **Как работает сборка мусора?**

1. **Вы создаёте объекты.**
    - Например, когда вы пишете `new Object()`, объект появляется в памяти.
    - Эти объекты остаются там, пока вы их используете.

2. **Сборщик мусора ищет "ненужные" объекты.**
    - "Ненужный" объект — это тот, до которого больше нельзя добраться из вашего кода.  
        Например, если объект больше не имеет ссылок, то его никто не сможет использовать.
    
3. **Он освобождает память.**
    - Сборщик удаляет такие объекты, чтобы освободить место для новых.

**Общие принципы работы сборки мусора** [^2]
**Как Java решает, какие объекты удалить?** [^4]
**Что важно знать?[^5]**
### 3. **Этапы сборки мусора**
Garbage Collection делится на несколько этапов:
1. #### **Mark (Отметка)**
	- GC "обходит" все объекты, начиная с GC Roots, и помечает достижимые объекты.
	- Недостижимые объекты остаются "непомеченными".
2. #### **Sweep (Очистка)**
	- GC освобождает память, занятую объектами, которые не были помечены на предыдущем этапе.
1. #### **Compact (Компактизация)**
	- После очистки память может оказаться фрагментированной.
	- GC перемещает объекты, чтобы устранить "пробелы" и оптимизировать использование памяти.

### 4. ==**Типы сборки мусора **== 
1. #### **Minor GC (Молодая сборка мусора)**
	- Очищает только **молодое поколение** (Young Generation).
	- Вызывается часто, поскольку молодое поколение быстро заполняется.
	- Перемещает выжившие объекты в Survivor Spaces или старое поколение.
2. #### **Major GC (Старшая сборка мусора)**
	- Очищает **старое поколение** (Old Generation).
	- Происходит реже, но занимает больше времени.
	- Вызывает **остановку всех потоков (Stop-The-World pause)**.
3. #### **Full GC**
	- Полная сборка мусора, включающая очистку и молодого, и старого поколений.
	- Самый затратный тип сборки мусора.

### 5. **Алгоритмы сборки мусора**
В Java используются различные алгоритмы GC, каждый из которых предназначен для определённых задач.

1. #### **Serial GC**
	- **Особенности:**
	    - Однопоточный.
	    - Используется для небольших приложений или систем с ограниченными ресурсами.
	- **Применение:**
	    - JVM параметр: `-XX:+UseSerialGC`.


2. #### **Parallel GC**
	- **Особенности:**
	    - Использует несколько потоков для выполнения сборки мусора.
	    - Подходит для приложений с высокой нагрузкой.
	- **Применение:**
	    - JVM параметр: `-XX:+UseParallelGC`.


3. #### **CMS (Concurrent Mark-Sweep) GC**
	- **Особенности:**
	    - Выполняет этапы "отметки" и "очистки" параллельно с работой приложения.
	    - Снижает паузы Stop-The-World.
	- **Недостатки:**
	    - Не проводит компактизацию памяти, что может привести к фрагментации.
	- **Применение:**
	    - JVM параметр: `-XX:+UseConcMarkSweepGC`.

4. #### **G1 (Garbage First) GC**
	- **Особенности:**
	    - Делит кучу на регионы, которые очищаются выборочно, начиная с наиболее заполненных.
	    - Подходит для приложений с большими объемами данных.
	    - Уменьшает паузы Stop-The-World.
	- **Применение:**
	    - JVM параметр: `-XX:+UseG1GC`.

5. #### **ZGC (Z Garbage Collector)**
	- **Особенности:**
	    - Поддерживает большие объемы памяти (до терабайтов).
	    - Минимизирует паузы Stop-The-World (обычно <10 мс).
	    - Появился в Java 11.
	- **Применение:**
	    - JVM параметр: `-XX:+UseZGC`.

6. #### **Shenandoah GC**
	- **Особенности:**
	    - Похож на ZGC, но работает быстрее.
	    - Эффективен при работе с низкими задержками.
	- **Применение:**
	    - JVM параметр: `-XX:+UseShenandoahGC`.

### 6. **Мониторинг сборки мусора**
Чтобы анализировать работу GC, можно использовать:

- **JVM параметры:**
    - `-verbose:gc` — выводит информацию о сборке мусора.
    - `-XX:+PrintGCDetails` — детальная информация о работе GC.
- **Инструменты мониторинга:**
    - **VisualVM:** Для анализа работы памяти.
    - **JConsole:** Для мониторинга JVM в реальном времени.

### 7. **Пример сборки мусора**
[^1]

### 8. Советы по оптимизации работы GC
1. Выбирайте подходящий алгоритм GC в зависимости от потребностей приложения.
2. Уменьшайте количество долгоживущих объектов, чтобы избежать их перемещения в старое поколение.
3. Используйте пулы объектов и кэширование для оптимизации использования памяти.
4. Регулярно профилируйте приложение, чтобы анализировать работу GC.

---
### Итог
Garbage Collection в Java автоматизирует управление памятью, снижая сложность разработки приложений. Различные алгоритмы GC и их параметры позволяют настроить JVM под конкретные задачи, обеспечивая баланс между производительностью и использованием ресурсов.


[^1]:```java
	public class GarbageCollectionExample {
	    public static void main(String[] args) {
	        for (int i = 0; i < 100000; i++) {
	            String temp = new String("Garbage Collection Example " + i);
	        }
	        System.gc(); // Ручной вызов сборки мусора (не гарантирует выполнение)
	        System.out.println("Сборка мусора запущена");
	    }
	}
	```

[^2]:### **Общие принципы работы сборки мусора**
	
	1. **Достижимость объектов (Reachability):**
	    - Объект считается достижимым, если на него есть ссылка от другого объекта или из "корневого" объекта (**GC Roots**).
	    - Если объект недостижим, JVM считает, что он больше не нужен.
	
	2. **GC Roots:** GC начинается с анализа "корневых" объектов:
	    - Локальные переменные, находящиеся в стеке вызовов (Stack).
	    - Статические переменные классов.
	    - Ссылки из Native Method Stack.
	    - Активные потоки.
	
	3. **Этапы работы сборки мусора:** GC выполняет три основные операции:
	    - **Mark (Отметка):** Находит и помечает достижимые объекты.
	    - **Sweep (Очистка):** Удаляет объекты, которые не были помечены.
	    - **Compact (Компактизация):** Перемещает оставшиеся объекты, чтобы устранить фрагментацию памяти.

[^3]:
[^4]:### Как Java решает, какие объекты удалить?
	
	1. **Смотрит на ссылки.**
	    
	    - Если объект больше никому не нужен (на него нет ссылок), его можно удалить.
	2. **Обходит цепочки.**
	    
	    - Java начинает с корневых объектов (GC Roots) и проверяет, какие объекты ещё связаны с ними.
	    - Все, что не связано с корнями, считается "мусором".
[^5]:### Что важно знать?
	
	1. **Сборка мусора происходит автоматически.**
	    
	    - Вам не нужно думать о том, чтобы "удалить" объект вручную. Java делает это за вас.
	2. **Вы можете подсказать сборщику мусора.**
	    
	    - Метод `System.gc()` позволяет "намекнуть", что сейчас хорошее время для уборки. Но Java может проигнорировать этот намёк.
	3. **Не бойтесь утечек памяти.**
	    
	    - Если объект всё ещё имеет ссылку, он не будет удалён, даже если вы его уже не используете. Поэтому важно правильно управлять ссылками (например, очищать коллекции).
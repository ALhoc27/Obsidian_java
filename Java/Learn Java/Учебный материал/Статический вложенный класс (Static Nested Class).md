Статический вложенный класс (`static nested class`) — это класс, объявленный внутри другого класса с модификатором `static` (*но не внутри метода*). Он будет принадлежать внешнему классу, а не экземпляру. В отличие от не статического внутреннего класса, он **==не имеет прямой связи с экземпляром внешнего класса==**. 
> Статический класс виден в пределах того же пакета, что и внешний класс, и его члены могут быть использованы с использованием синтаксиса **`ВнешнийКласс`.`СтатическийКласс` (Не требует экземпляра внешнего класса) ^[Это делает его более похожим на обычный класс, но с логическим отношением к внешнему классу.]

> [!WARNING]
>    - **Статический вложенный класс ==может содержать== как статические, так и нестатические поля и методы.**
>    - Статический вложенный класс ==может содержать== члены **с любым модификатором доступа**. **(private, protected, public, default)**
><br>
>  - **Статический вложенный класс имеет доступ**:
> 	 - К статическим членам внешнего класса (напрямую)
> 	 - К не статическим полям или методам внешнего класса обращаться может ==**только через экземпляр**==[^1]
> <br>
>  - **Внешний класс имеет доступ к членам ==статического== внутреннего класса**: 
> 	 - К его **статическим членам** напрямую (**без создания экземпляра**)
> 	 - К нестатическим членам (**через экземпляр внутреннего класса**)
##### **Когда использовать:**[^3]

Статический внутренний класс позволяет объединить два тесно связанных класса в одном месте.[^5] Этот подход удобен, если классы тесно связаны по функциональности, но вложенный класс не нуждается в доступе к нестатическим членам внешнего класса.

1. **Для логического разделения:** Используется, когда класс является логической частью другого, но не зависит от его экземпляра.
2. **Для работы со статическими данными внешнего класса:** Статический вложенный класс удобно использовать для обработки или группировки данных, относящихся только к статическим членам внешнего класса.
3. **Для организации кода:** Удобно для предотвращения загромождения пространства имён, когда вложенный класс логически связан с внешним.
##### Реальный пример использования: (`Builder`-паттерна) [^4]

[^1]:##### Статический класс не может обращаться к не статическим полям или методам внешнего класса напрямую, так как не существует ссылки на его экземпляр.
	
	*Пример:*
	```java
	public class OuterClass {
	    static int staticVar = 10;
	    int instanceVar = 20;
	
	    static class StaticNestedClass {
	        void display() {
	            System.out.println("Static variable: " + staticVar); // Доступ к статической переменной
	            // System.out.println("Instance variable: " + instanceVar); // Ошибка: нет доступа
	        }
	    }
	}
	```
	
	только через экземпляр `new OuterClass().instanceVar);`
	```java
	public class OuterClass {
	    static int staticVar = 10;
	    int instanceVar = 20;
	
	    static class StaticNestedClass {
	        void display() {
	            System.out.println("Static variable: " + staticVar); // Доступ к статической переменной
	            System.out.println("Instance variable: " + new OuterClass().instanceVar); // обьект класса (экземпляр)
	        }
	    }
	}
	```
	
	или через экземпляр (внешнего класса переданного в аргументах) :
	```java
	public class OuterClass {
	    int instanceVar = 20;
	
	    static class StaticNestedClass {
	        void display(OuterClass outer) {
	            System.out.println("Instance variable: " + outer.instanceVar);
	        }
	    }
	}
	```

[^3]:### Применение статического вложенного класса
	##### **Когда использовать:**
	
	1. **Для логического разделения:** Используется, когда класс является логической частью другого, но не зависит от его экземпляра.
	2. **Для работы со статическими данными внешнего класса:** Статический вложенный класс удобно использовать для обработки или группировки данных, относящихся только к статическим членам внешнего класса.
	3. **Для организации кода:** Удобно для предотвращения загромождения пространства имён, когда вложенный класс логически связан с внешним.
	
	###### **Пример — Вложенный класс для обработки данных внешнего класса:**
	```java
	public class Database {
	    private static String dbName = "MyDatabase";
	
	    static class Query {
	        static void printDatabaseName() {
	            System.out.println("Database: " + dbName); // Доступ к статической переменной
	        }
	    }
	}
	
	public class Main {
	    public static void main(String[] args) {
	        Database.Query.printDatabaseName();
	    }
	}
	```


[^4]:### **Реальный пример использования:** (`Builder`-паттерна:)
	Статические вложенные классы часто используются для создания _Builder_ объектов.
	
	```java
	public class Car {
	    private String engine;
	    private int wheels;
	
	    // Статический вложенный класс
	    public static class Builder {
	        private String engine;
	        private int wheels;
	
	        public Builder setEngine(String engine) {
	            this.engine = engine;
	            return this;
	        }
	
	        public Builder setWheels(int wheels) {
	            this.wheels = wheels;
	            return this;
	        }
	
	        public Car build() {
	            Car car = new Car();
	            car.engine = this.engine;
	            car.wheels = this.wheels;
	            return car;
	        }
	    }
	
	    @Override
	    public String toString() {
	        return "Car [engine=" + engine + ", wheels=" + wheels + "]";
	    }
	}
	```
	
	***Использование:***
	```java
	public class Main {
	    public static void main(String[] args) {
	        Car car = new Car.Builder()
	                .setEngine("V8")
	                .setWheels(4)
	                .build();
	
	        System.out.println(car);
	    }
	}
	```

[^5]:*Пример:*
	```java
	public class OuterClass {
	    static class NestedHelper {
	        public static void printMessage() {
	            System.out.println("Helper message");
	        }
	    }
	}
	```
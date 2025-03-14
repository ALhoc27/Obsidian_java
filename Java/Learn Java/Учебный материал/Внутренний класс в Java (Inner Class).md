Внутренний класс (`inner class`) — это класс, который объявлен внутри другого класса без использования модификатора `static` (*но не в методе*). ==**Каждый экземпляр внутреннего класса связан с экземпляром внешнего его класса**==. Внутренний класс предоставляет логическую группировку для классов и методов, которые тесно связаны с внешним классом. но в отличии от статических вложенный классов, **имеет доступ ко всем членам внешнего класса, включая нестатические и приватные**.
> Доступность внутреннего класс определяется модификаторами доступа

> [!TIP]
> 
> - **Внутренний вложенный класс** может содержать **==нестатические поля и методы==** и ==**статические константы** (`static final`)==
> <br>
> - **Внутренний вложенный класс** может **==напрямую==** обращаться ко всем **нестатическим** и **статическим** членам внешнего класса независимо от модификаторов (`private`, `protected`, `default`, `public`) [^3]
> <br>
> - **Внешний класс имеет доступ к членам внутреннего класса**:
> 	- К его **статическим членам** напрямую (**без создания экземпляра**)
> 	- К нестатическим членам (**через экземпляр внутреннего класса**)

Внутренние классы удобны для реализации интерфейсов или абстрактных классов, особенно если эта реализация используетсятолько внутри внешнего класса, внутренние классы так же используются в фабричных методах и полезен при обработкисобытий.
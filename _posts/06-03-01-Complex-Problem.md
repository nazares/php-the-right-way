---
title: Комплексная проблема
isChild: true
anchor:  complex_problem
---

## Комплексная проблема {#complex_problem_title}

If you have ever read about Dependency Injection then you have probably seen the terms *"Inversion of Control"* or
*"Dependency Inversion Principle"*. These are the complex problems that Dependency Injection solves.

### Inversion of Control

Inversion of Control is as it says, "inverting the control" of a system by keeping organizational control entirely
separate from our objects. In terms of Dependency Injection, this means loosening our dependencies by controlling and
instantiating them elsewhere in the system.

For years, PHP frameworks have been achieving Inversion of Control, however, the question became, which part of control
are we inverting, and where to? For example, MVC frameworks would generally provide a super object or base controller
that other controllers must extend to gain access to its dependencies. This **is** Inversion of Control, however,
instead of loosening dependencies, this method simply moved them.

Dependency Injection allows us to more elegantly solve this problem by only injecting the dependencies we need, when we
need them, without the need for any hard coded dependencies at all.

### S.O.L.I.D.

#### Single Responsibility Principle

The Single Responsibility Principle is about actors and high-level architecture. It states that “A class should have
only one reason to change.” This means that every class should _only_ have responsibility over a single part of the
functionality provided by the software. The largest benefit of this approach is that it enables improved code
_reusability_. By designing our class to do just one thing, we can use (or re-use) it in any other program without
changing it.

#### Open/Closed Principle

<<<<<<< Updated upstream
<<<<<<< Updated upstream
The Open/Closed Principle is about class design and feature extensions. It states that “Software entities (classes,
modules, functions, etc.) should be open for extension, but closed for modification.” This means that we should design
our modules, classes and functions in a way that when a new functionality is needed, we should not modify our existing
code but rather write new code that will be used by existing code. Practically speaking, this means that we should write
classes that implement and adhere to _interfaces_, then type-hint against those interfaces instead of specific classes.
=======
=======
>>>>>>> Stashed changes
Принцип открытости/закрытости касается проектирования классов и расширений функций. В нем говорится, что "программные объекты (классы,
модули, функции и т. д.) должны быть открыты для расширения, но закрыты для модификации". Это означает, что мы должны проектировать
наши модули, классы и функции таким образом, чтобы, когда потребуется новая функциональность, мы не должны были изменять наш существующий
код, а скорее писать новый код, который будет использоваться существующим кодом. С практической точки зрения это означает, что мы должны
писать классы, которые реализуют *интерфейсы* и придерживаются их, а затем указывать тип для этих интерфейсов, а не для конкретных классов.
<<<<<<< Updated upstream
>>>>>>> Stashed changes
=======
>>>>>>> Stashed changes

Самым большим преимуществом этого подхода является то, что мы можем очень легко расширить наш код с поддержкой чего-то нового, не изменяя
существующий код, а это означает, что мы можем сократить время контроля качества, а риск негативного воздействия на приложение существенно
снижается. Мы можем развертывать новый код быстрее и с большей уверенностью.

#### Принцип замены Лисков

Принцип замены Лисков касается подтипов и наследования. В нем говорится, что "дочерние классы никогда не должны нарушать
определения типов родительского класса". Или, говоря словами Robert C. Martin, "подтипы должны быть взаимозаменяемыми для своих базовых
типов".

Например, если у нас есть интерфейс `FileInterface`, который определяет метод `embed()`, и у нас есть классы `Audio` и `Video`,
которые оба реализуют интерфейс `FileInterface`, то мы можем ожидать, что использование Метод `embed()` всегда будет делать
то, что мы намеревались. Если позже мы создадим класс `PDF` или класс `Gist`, которые реализуют интерфейс `FileInterface`,
мы уже будем знать и понимать, что будет делать метод `embed()`. Самым большим преимуществом этого подхода является то,
что у нас есть возможность создавать гибкие и легко настраиваемые программы, потому что, когда мы меняем один объект
типа (например, `FileInterface`) на другой, нам не нужно ничего менять в нашей программе.

#### Принцип разделения интерфейса

<<<<<<< Updated upstream
<<<<<<< Updated upstream
The Interface Segregation Principle (ISP) is about _business-logic-to-clients_ communication. It states that “No client
should be forced to depend on methods it does not use.” This means that instead of having a single monolithic interface
that all conforming classes need to implement, we should instead provide a set of smaller, concept-specific interfaces
that a conforming class implements one or more of.
=======
=======
>>>>>>> Stashed changes
Принцип разделения интерфейса (ISP) касается связи *бизнес-логики с клиентами*. В нем говорится, что "Ни один клиент
не должен зависеть от методов, которые он не использует". Это означает, что вместо единого монолитного интерфейса,
который должны реализовать все соответствующие классы, мы должны вместо этого предоставить набор меньших интерфейсов,
зависящих от концепции, один или несколько из которых реализует соответствующий класс.
<<<<<<< Updated upstream
>>>>>>> Stashed changes
=======
>>>>>>> Stashed changes

Например, классу `Car` или `Bus` будет интересен метод `SteeringWheel()`, а классу `Motorcycle` или `Tricycle` — нет.
И наоборот, классу `Motorcycle` или `Tricycle` будет интересен метод `handlebars()`, а классу `Car` или `Bus` — нет.
Нет необходимости, чтобы все эти типы транспортных средств поддерживали как `steeringWheel()`, так и `handlebars()`,
поэтому мы должны разделить исходный интерфейс.

#### Принцип инверсии зависимости

Принцип инверсии зависимостей заключается в удалении жестких ссылок между отдельными классами, чтобы можно было использовать новые функции,
передавая другой класс. В нем говорится, что нужно *"Зависеть от абстракций. Не зависеть от конкретики"*.
Проще говоря, это означает, что наши зависимости должны быть интерфейсами/контрактами или абстрактными классами,
а не конкретными реализациями. Мы можем легко реорганизовать приведенный выше пример, чтобы следовать этому принципу.

{% highlight php %}
<?php
namespace Database;

class Database
{
    protected $adapter;

    public function __construct(AdapterInterface $adapter)
    {
        $this->adapter = $adapter;
    }
}

interface AdapterInterface {}

class MysqlAdapter implements AdapterInterface {}
{% endhighlight %}

Теперь у класса `Database` есть несколько преимуществ, зависящих от интерфейса, а не от конкретизации.

Учтите, что мы работаем в команде, а над адаптером работает коллега. В нашем первом примере нам
пришлось бы ждать, пока указанный коллега закончит работу над адаптером, прежде чем мы сможем должным образом смоделировать
его для наших модульных тестов. Теперь, когда зависимость представляет собой интерфейс/контракт, мы можем с радостью
создать макет этого интерфейса, зная, что наш коллега создаст адаптер на основе этого контракта.

Еще большее преимущество этого метода заключается в том, что наш код стал намного более масштабируемым. Если через год мы решим,
что хотим перейти на базу данных другого типа, мы можем написать адаптер, который реализует исходный интерфейс
и внедряет его вместо этого, больше не потребуется рефакторинг, поскольку мы можем гарантировать, что адаптер следует контракт,
установленный интерфейсом.

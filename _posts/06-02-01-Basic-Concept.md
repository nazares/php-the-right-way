---
title: Основная концепция
isChild: true
anchor:  basic_concept
---

## Основная концепция {#basic_concept_title}

Мы можем продемонстрировать концепцию, простым и примитивным примером.
У нас есть класс `Database`, который требует адаптер для общения с базой данных.
Here we have a `Database` class that requires an adapter to speak to the database. Мы реализуем адаптер в
конструкторе и создаем жесткую зависимость. Это делает тестирование сложным и означает что класс `Database`, очень тесно
связан с адаптером.

{% highlight php %}
<?php
namespace Database;

class Database
{
    protected $adapter;

    public function __construct()
    {
        $this->adapter = new MySqlAdapter;
    }
}

class MysqlAdapter {}
{% endhighlight %}

Этот код может быть переработан с использованием Внедрения Зависимости и следовательно ослабит зависимости.
Здесь мы внедряем зависимость в конструктор и используем [продвижение свойства конструктора][php-constructor-promotion], для того, чтобы оно было доступно во всем классе:

{% highlight php %}
<?php
namespace Database;

class Database
{
    public function __construct(protected MySqlAdapter $adapter)
    {

    }
}

class MysqlAdapter {}
{% endhighlight %}

Теперь мы отдаем классу `Database` его зависимость а не создаем его самого. Мы даже могли бы создать метод который принимал бы аргумент зависимости и устанавливал его этим способом, или если свойство `$adapter` было `public`, мы могли бы установить его напрямую.

[php-constructor-promotion]: https://www.php.net/manual/en/language.oop5.decon.php#language.oop5.decon.constructor.promotion

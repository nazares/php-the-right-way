---
isChild: true
title:   Взаимодействие с базами данных
anchor:  databases_interacting
---

## Взаимодействие с базами данных {#databases_interacting_title}

Когда разработчики впервые начинают изучать PHP, они часто заканчивают тем, что смешивают взаимодействие с базой данных
с логикой представления, используя код, который может выглядеть следующим образом:

```php
<ul>
<?php
foreach ($db->query('SELECT * FROM table') as $row) {
    echo "<li>".$row['field1']." - ".$row['field1']."</li>";
}
?>
</ul>
```

Это плохая практика по разным причинам, в основном из-за того, что ее трудно отлаживать, трудно тестировать, трудно читать,
и она будет выводить много полей, если вы не установите там ограничение.

Хотя есть много других решений для этого — в зависимости от того, предпочитаете ли вы [ООП]({{site.baseurl}}/#object-oriented-programming)
или [функциональное программирование]({{site.baseurl}}/#functional-programming) — должен быть какой-то элемент разделения.

```php
<?php
function getAllFoos($db) {
    return $db->query('SELECT * FROM table');
}

$results = getAllFoos($db);
foreach ($results as $row) {
    echo "<li>".$row['field1']." - ".$row['field1']."</li>"; // BAD!!
}
```

Это хорошее начало. Поместите эти два элемента в два разных файла, и вы получите четкое разделение.

Создайте класс для размещения этого метода, и у вас есть "Модель". Создайте простой файл `.php`, чтобы поместить в него
логику представления, и у вас будет "Представление", которое очень близко к [MVC] - общей архитектуре ООП для большинства
[фреймворков]({{site.baseurl}}/#frameworks).

**foo.php**

```php
<?php
$db = new PDO('mysql:host=localhost;dbname=testdb;charset=utf8mb4', 'username', 'password');

// Make your model available
include 'models/FooModel.php';

// Create an instance
$fooModel = new FooModel($db);
// Get the list of Foos
$fooList = $fooModel->getAllFoos();

// Show the view
include 'views/foo-list.php';
```

**models/FooModel.php**

```php
<?php
class FooModel
{
    public function __construct(protected PDO $db)
    {

    }

    public function getAllFoos() {
        return $this->db->query('SELECT * FROM table');
    }
}
```

**views/foo-list.php**

```php
<?php foreach ($fooList as $row): ?>
    <li><?= $row['field1'] ?> - <?= $row['field1'] ?></li>
<?php endforeach ?>
```

По сути, это то же самое, что и большинство современных фреймворков, хотя и немного более ручное. Возможно, вам не
нужно делать все это каждый раз, но смешивание слишком большого количества логики представления и взаимодействия с базой
данных может стать реальной проблемой, если вы когда-нибудь захотите [unit-тестирование]({{site.baseurl}}/#unit-testing) своего приложения.

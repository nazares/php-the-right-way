---
isChild: true
title:   Расширение PDO
anchor:  pdo_extension
---

## Расширение PDO {#pdo_extension_title}

[PDO] — это библиотека абстракции подключения к базе данных &mdash; встроен в PHP начиная с версии 5.1.0 &mdash; который
обеспечивает общий интерфейс для общения со многими различными базами данных. Например, вы можете использовать практически
идентичный код для взаимодействия с MySQL или SQLite:

{% highlight php %}
<?php
// PDO + MySQL
$pdo = new PDO('mysql:host=example.com;dbname=database', 'user', 'password');
$statement = $pdo->query("SELECT some_field FROM some_table");
$row = $statement->fetch(PDO::FETCH_ASSOC);
echo htmlentities($row['some_field']);

// PDO + SQLite
$pdo = new PDO('sqlite:/path/db/foo.sqlite');
$statement = $pdo->query("SELECT some_field FROM some_table");
$row = $statement->fetch(PDO::FETCH_ASSOC);
echo htmlentities($row['some_field']);
{% endhighlight %}

PDO не будет переводить ваши SQL-запросы или эмулировать отсутствующие функции; это исключительно для подключения к
нескольким типам баз данных с одним и тем же API.

Что еще более важно, `PDO` позволяет вам безопасно вводить чужие входные данные (например, ID) в ваши запросы SQL, не
беспокоясь об атаках путем внедрения SQL в базу данных. Это возможно с помощью операторов PDO и связанных параметров.

Предположим, PHP-скрипт получает числовой идентификатор в качестве параметра запроса. Этот идентификатор следует
использовать для извлечения записи пользователя из базы данных. Это `wrong` способ сделать это:

{% highlight php %}
<?php
$pdo = new PDO('sqlite:/path/db/users.db');
$pdo->query("SELECT name FROM users WHERE id = " . $_GET['id']); // <-- NO!
{% endhighlight %}

Это ужасный код. Вы вставляете необработанный параметр запроса в запрос SQL. Это позволит вам взломать систему в мгновение
ока, используя практику под названием [SQL Инъекции]. Только представьте, что хакер передает оригинальный параметр "id",
вызывая URL-адрес типа `http://domain.com/?id=1%3BDELETE+FROM+users`. Это установит для переменной `$_GET['id']` значение
`1;DELETE FROM users`, что удалит всех ваших пользователей! Вместо этого вы должны дезинфицировать ввод идентификатора,
используя параметры, привязанные к PDO.

{% highlight php %}
<?php
$pdo = new PDO('sqlite:/path/db/users.db');
$stmt = $pdo->prepare('SELECT name FROM users WHERE id = :id');
$id = filter_input(INPUT_GET, 'id', FILTER_SANITIZE_NUMBER_INT); // <-- filter your data first
(see [Data Filtering]({{site.baseurl}}#data_filtering)), especially important for INSERT, UPDATE, etc.
$stmt->bindParam(':id', $id, PDO::PARAM_INT); // <-- Automatically sanitized for SQL by PDO
$stmt->execute();
{% endhighlight %}

Это правильный код. Он использует связанный параметр в операторе PDO. Это ускользает от внешнего входного ID до того,
как он будет введен в базу данных, предотвращая потенциальные атаки SQL-инъекций.

Для записей, таких как INSERT или UPDATE, особенно важно сначала по-прежнему [фильтровать ваши данные](#data_filtering)
и очищать их для других вещей (удаление HTML-тегов, JavaScript и т. д.). PDO будет очищать его только для SQL, а не для
вашего приложения.

* [Узнать о PDO][pdo]

Вы также должны знать, что соединения с базой данных используют ресурсы, и не было ничего необычного в исчерпании ресурсов,
если соединения не были неявно закрыты, однако это было более распространено в других языках. Используя PDO, вы можете
неявно закрыть соединение, уничтожив объект, убедившись, что все оставшиеся ссылки на него удалены, т.е. установлены в
NULL. Если вы не сделаете это явно, PHP автоматически закроет соединение, когда ваш сценарий завершится - если, конечно,
вы не используете постоянные соединения.

* [Узнать о PDO соединениях]

[pdo]: https://www.php.net/pdo
[SQL Инъекции]: https://web.archive.org/web/20210413233627/http://wiki.hashphp.org/Validation
[Узнать о PDO соединениях]: https://www.php.net/pdo.connections

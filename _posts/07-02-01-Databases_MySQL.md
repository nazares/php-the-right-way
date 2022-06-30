---
title: Расширение MySQL
isChild: true
title:   MySQL Extension
anchor:  mysql_extension
---

## Расширение MySQL {#mysql_extension_title}

Расширение [mysql] для PHP невероятно старое и было заменено двумя другими расширениями:

- [mysqli]
- [pdo]

Разработка [mysql] была не только остановлена много лет назад но и было [deprecated начиная с PHP 5.5.0][mysql_deprecated],
и **было [официально удалено в PHP 7.0][mysql_removed]**.

Чтобы обезопасить вас от ковыряния в настройках `php.ini` и увидеть какой модуль вы используете, один из вариантов,
воспользоваться поиском для `mysql*` в вашем редакторе. Ели какая либо из функций таких как `mysql_connect()` и
`mysql_query()` появятся, то тогда `mysql` используется.

Даже если вы еще не используете PHP 7.x, если вы не позаботитесь об этом обновлении как можно скорее, это приведет к
большим трудностям, когда обновление PHP 7.x произойдет. Лучший вариант — заменить использование mysql на [mysqli] или
[PDO] в своих приложениях в соответствии с собственным графиком разработки, чтобы потом не торопиться.

**Если вы обновляетесь с [mysql] до [mysqli], остерегайтесь ленивых руководств по обновлению, которые предлагают вам
просто найти и заменить `mysql_*` на `mysqli_*`. Это не только грубое упрощение, но и упущенные преимущества,
предоставляемые mysqli, такие как привязка параметров, которая также предлагается в [PDO][pdo].**

- [MySQLi Prepared Statements][mysqli_prepared_statements]
- [PHP: Choosing an API for MySQL][mysql_api]

[mysql]: https://secure.php.net/mysqli
[mysql_deprecated]: https://secure.php.net/migration55.deprecated
[mysql_removed]: https://secure.php.net/manual/migration70.removed-exts-sapis.php
[mysqli]: https://secure.php.net/mysqli
[pdo]: https://secure.php.net/pdo
[mysql_api]: https://secure.php.net/mysqlinfo.api.choosing
[mysqli_prepared_statements]: https://websitebeaver.com/prepared-statements-in-php-mysqli-to-prevent-sql-injection

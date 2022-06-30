---
isChild: true
title:   MySQL Extension
anchor:  mysql_extension
---

## MySQL Extension {#mysql_extension_title}

The [mysql] extension for PHP is incredibly old and has been superseded by two other extensions:

- [mysqli]
- [pdo]

<<<<<<< Updated upstream
Not only did development stop long ago on [mysql], but it was [deprecated as of PHP 5.5.0]
[mysql_deprecated], and **has been [officially removed in PHP 7.0][mysql_removed]**.
=======
Разработка [mysql] была не только остановлена много лет назад но и было [deprecated начиная с PHP 5.5.0][mysql_deprecated], и **было [официально удалено в PHP 7.0][mysql_removed]**.
>>>>>>> Stashed changes

To save digging into your `php.ini` settings to see which module you are using, one option is to search for `mysql_*`
in your editor of choice. If any functions such as `mysql_connect()` and `mysql_query()` show up, then `mysql` is
in use.

<<<<<<< Updated upstream
Even if you are not using PHP 7.x yet, failing to consider this upgrade as soon as possible will lead to greater
hardship when the PHP 7.x upgrade does come about. The best option is to replace mysql usage with [mysqli] or [PDO] in
your applications within your own development schedules so you won't be rushed later on.
=======
Даже если вы еще не используете PHP 7.x, если вы не позаботитесь об этом обновлении как можно скорее, это приведет к большим
трудностям, когда обновление PHP 7.x произойдет. Лучший вариант — заменить использование mysql на [mysqli] или [PDO] в
своих приложениях в соответствии с собственным графиком разработки, чтобы потом не торопиться.
>>>>>>> Stashed changes

**Если вы обновляетесь с [mysql] до [mysqli], остерегайтесь ленивых руководств по обновлению, которые предлагают вам просто найти и заменить `mysql_*` на `mysqli_*`. Это не только грубое упрощение, но и упущенные преимущества, предоставляемые mysqli, такие как привязка параметров, которая также предлагается в [PDO][pdo].**

* [MySQLi Prepared Statements][mysqli_prepared_statements]
* [PHP: Choosing an API for MySQL][mysql_api]

[mysql]: https://secure.php.net/mysqli
[mysql_deprecated]: https://secure.php.net/migration55.deprecated
[mysql_removed]: https://secure.php.net/manual/migration70.removed-exts-sapis.php
[mysqli]: https://secure.php.net/mysqli
[pdo]: https://secure.php.net/pdo
[mysql_api]: https://secure.php.net/mysqlinfo.api.choosing
[mysqli_prepared_statements]: https://websitebeaver.com/prepared-statements-in-php-mysqli-to-prevent-sql-injection

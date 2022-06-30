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

Pазработка [mysql] была не только остановлена много лет назад но и было [deprecated начиная с PHP 5.5.0][mysql_deprecated], и **было [официально удалено в PHP 7.0][mysql_removed]**.

Чтобы обезопасить вас от ковыряния в настройках `php.ini` и увидеть какой модуль вы используете,
один из вариантов, воспользоваться поиском для `mysql*` в вашем редакторе. Ели какая либо из функций
таких как `mysql_connect()` и `mysql_query()` появятся, то тогда `mysql` используется.

Даже если вы еще не ипользуете PHP 7.x,
Even if you are not using PHP 7.x yet, failing to consider this upgrade as soon as possible will lead to greater
hardship when the PHP 7.x upgrade does come about. The best option is to replace mysql usage with [mysqli] or [PDO] in
your applications within your own development schedules so you won't be rushed later on.

**If you are upgrading from [mysql] to [mysqli], beware lazy upgrade guides that suggest you can simply find and replace `mysql_*` with `mysqli_*`. Not only is that a gross oversimplification, it misses out on the advantages that mysqli provides, such as parameter binding, which is also offered in [PDO][pdo].**

- [MySQLi Prepared Statements][mysqli_prepared_statements]
- [PHP: Choosing an API for MySQL][mysql_api]

[mysql]: https://secure.php.net/mysqli
[mysql_deprecated]: https://secure.php.net/migration55.deprecated
[mysql_removed]: https://secure.php.net/manual/migration70.removed-exts-sapis.php
[mysqli]: https://secure.php.net/mysqli
[pdo]: https://secure.php.net/pdo
[mysql_api]: https://secure.php.net/mysqlinfo.api.choosing
[mysqli_prepared_statements]: https://websitebeaver.com/prepared-statements-in-php-mysqli-to-prevent-sql-injection

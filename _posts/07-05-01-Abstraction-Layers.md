---
isChild: true
title:   Слои абстракций
anchor:  databases_abstraction_layers
---

## Слои абстракций {#databases_abstraction_layers_title}

Многие фреймворки предоставляют свой собственный уровень абстракции, который может располагаться или не располагаться
поверх [PDO][1]. Они часто будут эмулировать функции одной системы баз данных, отсутствующие в другой, оборачивая ваши
запросы в методы PHP, предоставляя вам реальную абстракцию базы данных, а не просто абстракцию соединения, которую
предоставляет PDO. Это, конечно, добавит немного накладных расходов, но если вы создаете переносимое приложение,
которое должно работать с MySQL, PostgreSQL и SQLite, то небольшие накладные расходы будут оправданы ради чистоты кода.

Некоторые уровни абстракции были построены с использованием стандартов пространств имен [PSR-0][psr0] или [PSR-4][psr4],
поэтому их можно установить в любое приложение, которое вам нравится:

* [Atlas][5]
* [Aura SQL][6]
* [Doctrine2 DBAL][2]
* [Medoo][8]
* [Propel][7]
* [laminas-db][4]

[1]: https://www.php.net/book.pdo
[2]: https://www.doctrine-project.org/projects/dbal.html
[4]: https://docs.laminas.dev/laminas-db/
[5]: https://atlasphp.io
[6]: https://github.com/auraphp/Aura.Sql
[7]: https://propelorm.org/
[8]: https://medoo.in/
[psr0]: https://www.php-fig.org/psr/psr-0/
[psr4]: https://www.php-fig.org/psr/psr-4/

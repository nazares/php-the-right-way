---
isChild: true
title: Фильтрация данных
anchor:  data_filtering
---

## Фильтрация данных (Data Filtering) {#data_filtering_title}

Никогда (никогда) не доверяйте чужому вводу, введенному в ваш PHP-код. Всегда очищайте и проверяйте внешний ввод перед
его использованием в коде. Функции `filter_var()` и `filter_input()` могут очищать текст и проверять текстовые форматы
(например, адреса электронной почты).

Внешний ввод может быть любым: `$_GET` и `$_POST` формируют входные данные, некоторые значения в суперглобальном массиве
`$_SERVER` и тело HTTP-запроса через `fopen('php://input', 'r')`. Помните, что внешний ввод не ограничивается данными
формы, отправленными пользователем. Загруженные и выгруженные файлы, значения сеанса, данные cookie и данные сторонних
веб-сервисов также являются посторонними входными данными.

Хотя сторонние данные можно хранить, комбинировать и обращаться к ним позже, они по-прежнему являются внешними входными
данными. Каждый раз, когда вы обрабатываете, выводите, объединяете или включаете данные в свой код, спрашивайте себя,
правильно ли фильтруются данные и можно ли им доверять.

Данные могут _фильтроваться_ по-разному в зависимости от их назначения. Например, когда нефильтрованный посторонний ввод
передается в вывод HTML-страницы, он может выполнять HTML и JavaScript на вашем сайте! Это известно как межсайтовый
скриптинг (XSS) и может быть очень опасной атакой. Один из способов избежать XSS — очистить все пользовательские данные
перед их выводом на вашу страницу, удалив теги HTML с помощью функции `strip_tags()` или экранировав символы со
специальным значением в соответствующие объекты HTML с помощью `htmlentities()` или функции `htmlspecialchars()`.

Другой пример — передача параметров для выполнения в командной строке. Это может быть чрезвычайно опасно (и, как правило,
это плохая идея), но вы можете использовать встроенную функцию `escapeshellarg()` для очистки аргументов выполняемой
команды.

Последний пример — прием внешнего ввода для определения файла для загрузки из файловой системы. Это можно использовать,
изменив имя файла на путь к файлу. Вам нужно удалить `"/"`, `"../"`, [null bytes][6] или другие символы из пути к файлу,
чтобы он не мог загружать скрытые, непубличные или конфиденциальные файлы.

* [Узнать о data filtering][1]
* [Узнать о `filter_var`][4]
* [Узнать о `filter_input`][5]
* [Узнать о handling null bytes][6]

### Санитарная обработка (Sanitization)

Дезинфекция удаляет (или избавляет от) незаконные или небезопасные символы из чужого ввода.

Например, вам необходимо санировать чужой ввод, прежде чем подключать ввод в HTML или вставлять это в необработанный SQL
запрос. Когда вы используете связанные параметры с [PDO](#databases), оно будет обеззараживать ввод для вас.

Иногда требуется разрешить несколько безопасных HTML тегов на входе, когда вкладываете их в HTML страницу. Это очень
сложно сделать и многие избегают этого, используя более ограниченное форматирование, такое как Markdown или BBCode, хотя
библиотеки белого списка, такие как [HTML Purifier][html-purifier] существуют по этой причине.

[Смотреть фильтры санирования][2]

### Unserialization

Опасно `unserialize()` данные от пользователей или других недоверенных ресурсов

It is dangerous to `unserialize()` data from users or other untrusted sources.  Doing so can allow malicious users to instantiate objects (with user-defined properties) whose destructors will be executed, **even if the objects themselves aren't used**.  You should therefore avoid unserializing untrusted data.

If you absolutely must unserialize data from untrusted sources, use PHP 7's [`allowed_classes`][unserialize] option to restrict which object types are allowed to be unserialized.

### Validation

Validation ensures that foreign input is what you expect. For example, you may want to validate an email address, a
phone number, or age when processing a registration submission.

[See Validation Filters][3]

[1]: https://secure.php.net/book.filter
[2]: https://secure.php.net/filter.filters.sanitize
[3]: https://secure.php.net/filter.filters.validate
[4]: https://secure.php.net/function.filter-var
[5]: https://secure.php.net/function.filter-input
[6]: https://secure.php.net/security.filesystem.nullbytes
[html-purifier]: http://htmlpurifier.org/
[unserialize]: https://secure.php.net/manual/function.unserialize.php

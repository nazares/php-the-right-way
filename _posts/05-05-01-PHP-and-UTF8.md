---
title:   Работа с UTF-8
isChild: true
anchor:  php_and_utf8
---

## Работа с UTF-8 {#php_and_utf8_title}

_Этот раздел был первоначально написан [Alex Cabal](https://alexcabal.com/) по адресу
[Лучшие практики PHP](https://phpbestpractices.org/#utf-8) и использовались в качестве основы для наших собственных рекомендаций по UTF-8_.

### Здесь нет краткости. Будьте внимательны, подробны и последовательны

В данный момент PHP не поддерживает Unicode на низком уровне. Есть несколько способов обеспечения
корректной обработки строк UTF-8, но это не легко, и требуется копаться, почти во всех уровнях
веб-приложения, начиная с HTML до SQL и PHP. Мы будем стремиться
к краткому практическому изложению.

### UTF-8 на уровне PHP

Базовые операции со строками, такие как конкатенация двух строк и присваивание строк к переменным,
не требуют ничего специально для UTF-8. Однако, большинство строковых функций, как `strpos()` и `strlen()`, требуют специальных решений. Эти функции часто имеют приставку `mb_*`: например,
`mb_strpos()` and `mb_strlen()`. Эти `mb_*` строки доступны вам через [Multibyte String Extension],
и специально разработаны для операций со строками Unicode.

Вы должны использовать `mb_*` функции каждый раз когда оперируете над Unicode строками. Например
если вы будете использовать `substr()` с UTF-8 строкой, существует большой риск, того, что результат
будет содержать некоторые искаженные полу-символы. Правильной для использования функцией будет,
мультибайтовая пара, `mb_substr()`.

Сложная часть - постоянно помнить об использовании `mb_*` функций. Если вы забудете даже один раз,ваша Unicode
строка имеет шанс быть искаженной при дальнейшей обработке.

Не все строковые функции имеют дополнение `mb_*`. Если его нет, для того что вы хотите, тогда вам просто не повезло.

Необходимо использовать функцию `mb_internal_encoding()` в начале каждого, написанного вами скрипта PHP (или в начале
глобально подключенного скрипта), и прямо следом функцию `mb_http_output()`, если ваш скрипт выводится в браузер.
Четкое определение кодировки ваших скриптов спасет вас от большого количества головной боли.

Более того, многие PHP функции которые оперируют со строками имеют необязательный параметр, позволяющий вам определять кодировку символа. Вы должны всегда четко указывать UTF-8, когда
предоставляется возможность. Например, `htmlentities()` имеет параметр для кодировки символа, и вы всегда должны указывать UTF-8, если имеете дело с такими строками. Обратите внимание что начиная с PHP 5.4.0, UTF-8 кодировка по-умолчанию для `htmlentities()` и `htmlspecialchars()`.

И наконец, если вы создаете распространяемое приложение и не можете быть уверены что расширение `mbstring` будет включено, тогда рассмотрите использование [symfony/polyfill-mbstring] пакета Composer. Он будет использовать `mbstring`, когда доступно, и вернется к не UTF-8 функциям если нет.

[Multibyte String Extension]: https://secure.php.net/book.mbstring
[symfony/polyfill-mbstring]: https://packagist.org/packages/symfony/polyfill-mbstring

### UTF-8 на уровне Базы Данных

Если ваш PHP скрипт обращается к MySQL, есть шанс что ваши строки будут храниться как не-UTF-8 строки в базе данных
даже если вы следовали всем предостережениям выше.

Чтобы быть уверенным что ваши строки предаются от PHP к MySQL как UTF-8, убедитесь в том что ваша база данных и таблицы установлены в `utf8mb4` набор символов и сопоставление, и то что вы используете набор символов `utf8mb4` в строке подключения PDO. Смотрите пример ниже. Это _критически важно_.

Обратите внимание что вы должны использовать набор символов `utf8mb4` для полноценной поддержки UTF-8, а не `utf8`! [Смотрите дальнейшее чтение](#further-reading-utf8)
чтобы узнать почему.

### UTF-8 на уровне браузера

Используйте `mb_http_output()` функцию чтобы обеспечить UTF-8 вывод вашего PHP скрипта в браузер.

Затем браузер должен будет сообщить ответом HTTP, что эту страницу следует рассматривать как UTF-8. Сегодня принято устанавливать набор символов в заголовке ответа HTTP следующим образом:

{% highlight php %}
<?php
header('Content-Type: text/html; charset=UTF-8')
{% endhighlight %}

Исторический подход к этому заключался в том, чтобы включить [тег charset `<meta>`](http://htmlpurifier.org/docs/enduser-utf8.html) в тег `<head>` вашей страницы.

{% highlight php %}
<?php
// Tell PHP that we're using UTF-8 strings until the end of the script
mb_internal_encoding('UTF-8');
$utf_set = ini_set('default_charset', 'utf-8');
if (!$utf_set) {
    throw new Exception('could not set default_charset to utf-8, please ensure it\'s set on your system!');
}

// Tell PHP that we'll be outputting UTF-8 to the browser
mb_http_output('UTF-8');

// Our UTF-8 test string
$string = 'Êl síla erin lû e-govaned vîn.';

// Transform the string in some way with a multibyte function
// Note how we cut the string at a non-Ascii character for demonstration purposes
$string = mb_substr($string, 0, 15);

// Connect to a database to store the transformed string
// See the PDO example in this document for more information
// Note the `charset=utf8mb4` in the Data Source Name (DSN)
$link = new PDO(
    'mysql:host=your-hostname;dbname=your-db;charset=utf8mb4',
    'your-username',
    'your-password',
    array(
        PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
        PDO::ATTR_PERSISTENT => false
    )
);

// Store our transformed string as UTF-8 in our database
// Your DB and tables are in the utf8mb4 character set and collation, right?
$handle = $link->prepare('insert into ElvishSentences (Id, Body, Priority) values (default, :body, :priority)');
$handle->bindParam(':body', $string, PDO::PARAM_STR);
$priority = 45;
$handle->bindParam(':priority', $priority, PDO::PARAM_INT); // explicitly tell pdo to expect an int
$handle->execute();

// Retrieve the string we just stored to prove it was stored correctly
$handle = $link->prepare('select * from ElvishSentences where Id = :id');
$id = 7;
$handle->bindParam(':id', $id, PDO::PARAM_INT);
$handle->execute();

// Store the result into an object that we'll output later in our HTML
// This object won't kill your memory because it fetches the data Just-In-Time to
$result = $handle->fetchAll(\PDO::FETCH_OBJ);

// An example wrapper to allow you to escape data to html
function escape_to_html($dirty){
    echo htmlspecialchars($dirty, ENT_QUOTES, 'UTF-8');
}

header('Content-Type: text/html; charset=UTF-8'); // Unnecessary if your default_charset is set to utf-8 already
?><!doctype html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>UTF-8 test page</title>
    </head>
    <body>
        <?php
        foreach($result as $row){
            escape_to_html($row->Body);  // This should correctly output our transformed UTF-8 string to the browser
        }
        ?>
    </body>
</html>
{% endhighlight %}

### Дальнейшее чтение {#further-reading-utf8}

* [PHP Manual: String Operations](https://secure.php.net/language.operators.string)
* [PHP Manual: String Functions](https://secure.php.net/ref.strings)
  * [`strpos()`](https://secure.php.net/function.strpos)
  * [`strlen()`](https://secure.php.net/function.strlen)
  * [`substr()`](https://secure.php.net/function.substr)
* [PHP Manual: Multibyte String Functions](https://secure.php.net/ref.mbstring)
  * [`mb_strpos()`](https://secure.php.net/function.mb-strpos)
  * [`mb_strlen()`](https://secure.php.net/function.mb-strlen)
  * [`mb_substr()`](https://secure.php.net/function.mb-substr)
  * [`mb_internal_encoding()`](https://secure.php.net/function.mb-internal-encoding)
  * [`mb_http_output()`](https://secure.php.net/function.mb-http-output)
  * [`htmlentities()`](https://secure.php.net/function.htmlentities)
  * [`htmlspecialchars()`](https://secure.php.net/function.htmlspecialchars)
* [Stack Overflow: What factors make PHP Unicode-incompatible?](https://stackoverflow.com/questions/571694/what-factors-make-php-unicode-incompatible)
* [Stack Overflow: Best practices in PHP and MySQL with international strings](https://stackoverflow.com/questions/140728/best-practices-in-php-and-mysql-with-international-strings)
* [How to support full Unicode in MySQL databases](https://mathiasbynens.be/notes/mysql-utf8mb4)
* [Bringing Unicode to PHP with Portable UTF-8](https://www.sitepoint.com/bringing-unicode-to-php-with-portable-utf8/)
* [Stack Overflow: DOMDocument loadHTML does not encode UTF-8 correctly](https://stackoverflow.com/questions/8218230/php-domdocument-loadhtml-not-encoding-utf-8-correctly)

---
isChild: true
title: Исключения
anchor:  exceptions
---

## Исключения {#exceptions_title}

Исключения являются стандартной частью большинства популярных языков программирования, но PHP-программисты часто упускают
их из виду.

Такие языки, как Ruby, очень сильно насыщенны исключениями, поэтому всякий раз, когда что-то идет не так, например, сбой
HTTP-запроса или запрос БД, или даже если ресурс изображения не может быть найден, Ruby (или используемые gems) выдает
исключение на экран, что означает, что вы сразу узнаете, что произошла ошибка.

PHP сам по себе довольно слаб с этим, и вызов `file_get_contents()` обычно просто дает вам `FALSE` и предупреждение.
Многие старые PHP-фреймворки, такие как CodeIgniter, просто вернут false, запишут сообщение в свои проприетарные журналы
и, возможно, позволят вам использовать такой метод, как `$this->upload->get_error()`, чтобы увидеть, что пошло не так.
Проблема здесь в том, что вам нужно искать ошибку и проверять документы, чтобы увидеть, какой метод ошибки используется
для этого класса, вместо того, чтобы делать это предельно очевидным.

Другая проблема — когда классы автоматически выбрасывают ошибку на экран и выходят из процесса. Когда вы делаете это,
вы мешаете другому разработчику динамически обрабатывать эту ошибку. Исключения должны создаваться, чтобы разработчики
знали об ошибке; затем они могут выбрать, как с этим справиться. Например.:

```php
<?php
$email = new Fuel\Email;
$email->subject('My Subject');
$email->body('How the heck are you?');
$email->to('guy@example.com', 'Some Guy');

try
{
    $email->send();
}
catch(Fuel\Email\ValidationFailedException $e)
{
    // The validation failed
}
catch(Fuel\Email\SendingFailedException $e)
{
    // The driver could not send the email
}
finally
{
    // Executed regardless of whether an exception has been thrown, and before normal execution resumes
}
```

### SPL Исключения

Общий класс `Exception` предоставляет разработчику очень мало контекста отладки; однако, чтобы исправить это, можно
создать специализированный тип `Exception`, создав подкласс общего класса `Exception`:

```php
<?php
class ValidationException extends Exception {}
```

Это означает, что вы можете добавить несколько блоков catch и по-разному обрабатывать разные исключения. Это может
привести к созданию _множества_ пользовательских исключений, некоторых из которых можно было бы избежать с помощью
исключений SPL, представленных в [расширении SPL][splext].

Если, например, вы используете магический метод `__call()` и запрошен недопустимый метод, то вместо того, чтобы
генерировать стандартное исключение, которое является расплывчатым, или создавать специальное исключение только для этого,
вы можете просто `throw new BadMethodCallException;`.

* [Читать о Exceptions][exceptions]
* [Читать о SPL Exceptions][splexe]
* [Nesting Exceptions In PHP][nesting-exceptions-in-php]

[splext]: /#standard_php_library
[exceptions]: https://www.php.net/language.exceptions
[splexe]: https://www.php.net/spl.exceptions
[nesting-exceptions-in-php]: https://www.brandonsavage.net/exceptional-php-nesting-exceptions-in-php/

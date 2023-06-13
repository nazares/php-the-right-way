---
title: Интерфейс командной строки
isChild: true
anchor:  command_line_interface
---

## Интерфейс командной строки {#command_line_interface_title}

PHP был создан чтобы писать веб-приложения, но он так же полезен для создания скриптовых программ с интерфейсом командной
строки (CLI). Программы командной строки PHP могут помочь автоматизировать общие задачи такие как тестирование,
разворачивание, и администрирование приложений.

Программы CLI PHP powerful потому что вы можете использовать код вашего приложения напрямую без необходимости создания и
защиты графического веб-интерфейса для него. Просто убедитесь в том что **не** положили ваши CLI PHP скрипты в корень
вашей общедоступной директории!

Попробуйте запустить PHP из командной строки:

{% highlight console %}
> php -i
{% endhighlight %}

Параметр `-i` выведет на экран вашу конфигурацию PHP также как функция [`phpinfo()`][phpinfo].

Параметр `-a` предоставляет интерактивную среду, похоже на ruby's IRB или на интерактивную среду python. Есть также ряд
других полезных [параметров командной строки][cli-options].

Давайте напишем простую "Hello, $name" CLI программу. Попробуйте создать файл с именем `hello.php` как показано ниже.

{% highlight php %}
<?php
if ($argc !== 2) {
    echo "Usage: php hello.php <name>" . PHP_EOL;
    exit(1);
}
$name = $argv[1];
echo "Hello, $name" . PHP_EOL;
{% endhighlight %}

PHP установит две специальные переменные, основываясь на аргументах с которыми вы выполнили скрипт.  [`$argc`][argc] -
это целочисленная переменная содержащая аргумент *count* (количество) и [`$argv`][argv] - это переменная - массив
содержащий значение *value* каждого из аргументов. Первый аргумент - это всегда имя файла PHP скрипта, в данном случае
`hello.php`.

Выражение `exit()` используется с не нулевым (non-zero) числом чтобы дать понять командной оболочке когда команда
завершилась неудачей. Обычно используемые коды выходов могут быть найдены [здесь][exit-codes].

Чтобы запустить наш скрипт ниже, из командной строки:

{% highlight console %}
> php hello.php
Usage: php hello.php <name>
> php hello.php world
Hello, world
{% endhighlight %}

 * [Узнать о запуске PHP из командной строки][php-cli]

[phpinfo]: https://www.php.net/function.phpinfo
[cli-options]: https://www.php.net/features.commandline.options
[argc]: https://www.php.net/reserved.variables.argc
[argv]: https://www.php.net/reserved.variables.argv
[exit-codes]: https://www.gsp.com/cgi-bin/man.cgi?section=3&amp;topic=sysexits
[php-cli]: https://www.php.net/features.commandline.options

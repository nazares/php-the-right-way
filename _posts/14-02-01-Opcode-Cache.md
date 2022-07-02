---
isChild: true
anchor:  opcode_cache
---

## Opcode Cache {#opcode_cache_title}

Когда файл PHP выполняется, он должен быть сначала скомпилирован в
[opcodes](https://secure.php.net/manual/internals2.opcodes.php) (инструкции машинного языка для ЦП). Если исходный
код не изменился, коды операций будут такими же, поэтому этот шаг компиляции становится пустой тратой ресурсов процессора.

Кэш opcode операций предотвращает избыточную компиляцию, сохраняя opcodes в памяти и повторно используя их при
последовательных вызовах. Обычно он сначала проверяет подпись или время модификации файла, если были какие-либо изменения.

Вполне вероятно, что кеш opcode операции значительно улучшит скорость вашего приложения. Начиная с PHP 5.5 есть
встроенный — [Zend OPcache][opcache-book]. В зависимости от вашего пакета/дистрибутива PHP он обычно включен по умолчанию
— проверьте [opcache.enable](https://secure.php.net/manual/opcache.configuration.php#ini.opcache.enable) и вывод
`phpinfo()`, чтобы убедиться. Для более ранних версий есть расширение PECL.

Подробнее о кэшах opcodes:

* [Zend OPcache][opcache-book] (bundled with PHP since 5.5)
* Zend OPcache (formerly known as Zend Optimizer+) is now [open source][Zend Optimizer+]
* [APC] - PHP 5.4 and earlier
* [XCache]
* [WinCache] (extension for MS Windows Server)
* [list of PHP accelerators on Wikipedia][PHP_accelerators]
* [PHP Preloading] - PHP >= 7.4

[opcache-book]: https://secure.php.net/book.opcache
[APC]: https://www.php.net/book.apcu
[XCache]: https://xcache.lighttpd.net/
[Zend Optimizer+]: https://github.com/zendtech/ZendOptimizerPlus
[WinCache]: https://www.iis.net/downloads/microsoft/wincache-extension
[PHP_accelerators]: https://wikipedia.org/wiki/List_of_PHP_accelerators
[PHP Preloading]: https://www.php.net/opcache.preloading

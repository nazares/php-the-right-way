---
title: Windows Установка
isChild: true
anchor:  windows_setup
---

## Windows Установка {#windows_setup_title}

Вы можете скачать бинарники из [windows.php.net/download][php-downloads]. После извлечения PHP, рекомендуется установить [PATH][windows-path] на коневую папку PHP (где находится php.exe) для того чтобы вы могли выполнять PHP из любого места.

Для изучения и локальной разработки, вы можете использовать встроенный веб-сервер с PHP 5.4+ так что вам не нужно беспокоиться об
этой настройке. Если вы хотите что-то наподобие "все в одном", которое включало бы полноценный веб-сервер а также MySQL, тогда такие инструменты
как [XAMPP][xampp], [EasyPHP][easyphp], [OpenServer][openserver] и [WAMP][wamp] помогут
быстро настроить и запустить среду разработки Windows. Тем не менее, эти инструменты будут немного отличаться от
production, так что будьте осторожны с различиями в средах, если вы работаете в Windows, а развертывание производите в Linux.

Если вам нужно запустить свою production систему в Windows, тогда IIS7 даст вам самую лучшую стабильность и производительность. Вы
можете использовать [phpmanager][phpmanager] (GUI плагин для IIS7) для того чтобы упростить настройку и управление PHP. IIS7 поставляется со
встроенным FastCGI и готов к работе, вам просто нужно настроить PHP обработчик. Для поддержки и дополнительных ресурсов
есть [выделенная область на iis.net][php-iis] for PHP.

Как правило, запуск вашего приложения в разных средах разработки и production может привести к появлению странных ошибок
запуска. Если вы разрабатываете в Windows а развертывание осуществляете Linux (или на чем-нибудь не-Windows) тогда вам следует рассмотреть возможность использования [Virtual Machine](/#virtualization_title).

У Chris Tankersley есть очень полезный пост в блоге о том, какие инструменты он использует для [PHP разработки в Windows][windows-tools].

[easyphp]: http://www.easyphp.org/
[phpmanager]: http://phpmanager.codeplex.com/
[openserver]: http://open-server.ru/
[wamp]: http://www.wampserver.com/en/
[php-downloads]: http://windows.php.net/download/
[php-iis]: http://php.iis.net/
[windows-path]: http://www.windows-commandline.com/set-path-command-line/
[windows-tools]: http://ctankersley.com/2016/11/13/developing-on-windows-2016/
[xampp]: http://www.apachefriends.org/en/xampp.html

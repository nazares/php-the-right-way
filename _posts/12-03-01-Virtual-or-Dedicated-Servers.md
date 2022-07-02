---
title:  Виртуальные или выделенные серверы
isChild: true
anchor:  virtual_or_dedicated_servers
---

## Виртуальные или выделенные серверы {#virtual_or_dedicated_servers_title}

Если вы знакомы с системным администрированием или заинтересованы в его изучении, виртуальные или выделенные серверы
дадут вам полный контроль над производственной средой вашего приложения.

### nginx и PHP-FPM

PHP через встроенный в PHP диспетчер процессов FastCGI (FPM) очень хорошо сочетается с [nginx], который представляет
собой легкий высокопроизводительный веб-сервер. Он использует меньше памяти, чем Apache, и может лучше обрабатывать
больше одновременных запросов. Это особенно важно для виртуальных серверов, у которых не так много свободной памяти.

* [Читать больше о nginx][nginx]
* [Читать больше о PHP-FPM][phpfpm]
* [Узнайте больше о безопасной настройке nginx и PHP-FPM.][secure-nginx-phpfpm]

### Apache и PHP

PHP и Apache имеют долгую совместную историю. Apache легко настраивается и имеет множество доступных
[модулей][apache-modules] для расширения функциональности. Это популярный выбор для общих серверов и простая настройка
для PHP-фреймворков и приложений с открытым исходным кодом, таких как WordPress. К сожалению, по умолчанию Apache
использует больше ресурсов, чем nginx, и не может обрабатывать столько посетителей одновременно.

Apache есть несколько возможных конфигураций для запуска PHP. Наиболее распространенным и простым в настройке является
[prefork MPM] с mod_php5. Хотя это не самое эффективное использование памяти, это самое простое в работе и использовании.
Это, вероятно, лучший выбор, если вы не хотите слишком углубляться в аспекты администрирования сервера. Обратите внимание,
что если вы используете mod_php5, вы ДОЛЖНЫ использовать prefork MPM.

В качестве альтернативы, если вы хотите выжать из Apache больше производительности и стабильности, вы можете
воспользоваться той же системой FPM, что и nginx, и запустить [worker MPM] или [event MPM] с mod_fastcgi или mod_fcgid.
Эта конфигурация будет значительно более эффективной с точки зрения использования памяти и намного быстрее, но ее
настройка потребует больше усилий.

Если вы используете Apache 2.4 или более позднюю версию, вы можете использовать [mod_proxy_fcgi], чтобы получить отличную
производительность, которую легко настроить.

* [Читать больше о Apache][apache]
* [Читать больше о Multi-Processing Modules][apache-MPM]
* [Читать больше о mod_fastcgi][mod_fastcgi]
* [Читать больше о mod_fcgid][mod_fcgid]
* [Читать больше о mod_proxy_fcgi][mod_proxy_fcgi]
* [Читать больше о setting up Apache and PHP-FPM with mod_proxy_fcgi][tutorial-mod_proxy_fcgi]

[nginx]: https://nginx.org/
[phpfpm]: https://secure.php.net/install.fpm
[secure-nginx-phpfpm]: https://nealpoole.com/blog/2011/04/setting-up-php-fastcgi-and-nginx-dont-trust-the-tutorials-check-your-configuration/
[apache-modules]: https://httpd.apache.org/docs/2.4/mod/
[prefork MPM]: https://httpd.apache.org/docs/2.4/mod/prefork.html
[worker MPM]: https://httpd.apache.org/docs/2.4/mod/worker.html
[event MPM]: https://httpd.apache.org/docs/2.4/mod/event.html
[apache]: https://httpd.apache.org/
[apache-MPM]: https://httpd.apache.org/docs/2.4/mod/mpm_common.html
[mod_fastcgi]: https://blogs.oracle.com/opal/entry/php_fpm_fastcgi_process_manager
[mod_fcgid]: hhttps://httpd.apache.org/mod_fcgid/
[mod_proxy_fcgi]: https://httpd.apache.org/docs/current/mod/mod_proxy_fcgi.html
[tutorial-mod_proxy_fcgi]: https://serversforhackers.com/video/apache-and-php-fpm

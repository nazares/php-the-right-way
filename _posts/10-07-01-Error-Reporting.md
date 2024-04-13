---
isChild: true
title: Отчет об ошибках
anchor:  error_reporting
---

## Отчет об ошибках {#error_reporting_title}

Регистрация ошибок может быть полезна для поиска проблемных мест в вашем приложении, но она также может предоставить
информацию о структуре вашего приложения для внешнего мира. Чтобы эффективно защитить ваше приложение от проблем, которые
могут быть вызваны выводом этих сообщений, вам необходимо по-разному настроить сервер для разработки и производства
(в реальном времени).

### Разработка

Чтобы показать все возможные ошибки во время **разработки**, настройте следующие параметры в файле `php.ini`:

```ini
display_errors = On
display_startup_errors = On
error_reporting = -1
log_errors = On
```

> Передача значения `-1` покажет все возможные ошибки, даже если в будущих версиях PHP будут добавлены новые уровни и
> константы. Константа `E_ALL` также ведет себя так, начиная с PHP 5.4. -
> [php.net](https://www.php.net/ru/function.error-reporting)

Константа уровня ошибки `E_STRICT` была введена в 5.3.0 и не является частью `E_ALL`, однако она стала частью `E_ALL` в
5.4.0. Что это значит? С точки зрения сообщения о каждой возможной ошибке в версии 5.3 это означает, что вы должны
использовать либо `-1`, либо `E_ALL | E_STRICT`.

**Отчет о каждой возможной ошибке по версии PHP**

* &lt; 5.3 `-1` or `E_ALL`
* &nbsp; 5.3 `-1` or `E_ALL | E_STRICT`
* &gt; 5.3 `-1` or `E_ALL`

### Производство

Чтобы скрыть ошибки в вашей **производственной** среде, настройте файл `php.ini` следующим образом:

```ini
display_errors = Off
display_startup_errors = Off
error_reporting = E_ALL
log_errors = On
```

При использовании этих настроек ошибки по-прежнему будут регистрироваться в журналах ошибок веб-сервера, но не будут
отображаться пользователю. Дополнительные сведения об этих настройках см. в руководстве по PHP:

* [error_reporting](https://www.php.net/ru/errorfunc.configuration#ini.error-reporting)
* [display_errors](https://www.php.net/ru/errorfunc.configuration#ini.display-errors)
* [display_startup_errors](https://www.php.net/ru/errorfunc.configuration#ini.display-startup-errors)
* [log_errors](https://www.php.net/ru/errorfunc.configuration#ini.log-errors)

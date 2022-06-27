---
isChild: true
anchor:  mac_setup
---

## Mac Установка {#mac_setup_title}

macOS поставляется с предустановленным PHP но это обычно немного более ранняя версия чем последний стабильный релиз. Есть есколько способов установить последнюю версию PHP в macOS.

### Установка PHP через Homebrew

[Homebrew] - это пакетный менеджер для macOS который помогает вам легко установить PHP и различные расширения. Главный репозиторий Homebrew предоставляет "formulae" формулы для PHP 5.6, 7.0, 7.1, 7.2, 7.3, 7.4, 8.0 и PHP 8.1. Установите последнюю версию командой:

    brew install php@8.1

Вы можете переключаться между Homebrew PHP вырсиями изменяя переменную `PATH`. Как альтернативу, вы можете использовать [brew-php-switcher][brew-php-switcher] для переключения PHP версий автоматически.

Также вы можете переключаться вручную между PHP версиями, отсоединяяя и присоединяя желаемую версию:

    brew unlink php
    brew link --overwrite php@8.0

    brew unlink php
    brew link --overwrite php@8.1

### Установка PHP через Macports

Проект [MacPorts] - это инициатива open-source сообщества направленная на разработку
простой в использовании системы для компиляции, установки, и обновления ПО с отрытым исходным кодом,
на основе командной строки, X11 или Aqua в операционной системе OS X.

MacPorts поддерживает предварительно скомпилированные бинарники, поэтому вам не нужно пересобирать каждую
зависимость из исходных tarball файлов, это спасет вас если в вашей системе не установлен какой-либо пакет..

Здесь вы можете установить `php54`, `php55`, `php56`, `php70`, `php71`, `php72`, `php73`, `php74`, `php80` или `php81` используя команду `port install`, например:

    sudo port install php74
    sudo port install php81

И вы можете запустить команду `select` чтобы переключиться на активную версию PHP:

    sudo port select --set php php81

### Установка PHP через phpbrew

[phpbrew] это инструмент для установки и управления несколькими версиями PHP. Это может быть реально полезным, когда два разных
приложения/проекта требуют разных версий PHP, и вы не используете виртуальные машины.

### Установка PHP через бинарный установщик Liip

Еще один популярный способ - это [php-osx.liip.ch] который обеспечивает методы установки в одну строку для версий с 5.3 по 7.3.
Это не перезаписывает бинарники PHP установленные Apple, а устанавливает все в отдельные места (/usr/local/php5).

### Сборка из исходников

Еще один метод, который дает вам контроль над версией PHP, которую вы устанавливаете, это [сделай сам][mac-compile].
В этом случае, также обязательно установите [Xcode][xcode-gcc-substitution] или заменитель
["Command Line Tools for XCode"] скачиваемый из Apple's Mac Developer Center.

### Универсальные установщики

Перечисленные выше решения в основном обрабатывают сам PHP и не предоставляют такие вещи как [Apache][apache], [Nginx][nginx] или SQL-сервер.
Решения "Все в одном" такие как [MAMP][mamp-downloads] или [XAMPP][xampp] установят для вас те другие части  программного обеспечения
и свяжут их все вместе, но простота настройки идет в ущерб гибкости.

[Homebrew]: https://brew.sh/
[Homebrew PHP]: https://github.com/Homebrew/homebrew-php#installation
[MacPorts]: https://www.macports.org/install.php
[phpbrew]: https://github.com/phpbrew/phpbrew
[php-osx.liip.ch]: https://php-osx.liip.ch/
[mac-compile]: https://secure.php.net/install.macosx.compile
[xcode-gcc-substitution]: https://github.com/kennethreitz/osx-gcc-installer
["Command Line Tools for XCode"]: https://developer.apple.com/downloads
[apache]: https://httpd.apache.org/
[nginx]: https://www.nginx.com/
[mamp-downloads]: https://www.mamp.info/en/downloads/
[xampp]: https://www.apachefriends.org/index.html
[brew-php-switcher]: https://github.com/philcook/brew-php-switcher

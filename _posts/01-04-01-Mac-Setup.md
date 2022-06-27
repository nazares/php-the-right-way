---
isChild: true
anchor:  mac_setup
---

## Mac Установка {#mac_setup_title}

macOS поставляется с предустановленным PHP но это обычно немного более ранняя версия чем последний стабильный релиз. Есть есколько способов установить последнюю версию PHP в macOS.

### Установка PHP через Homebrew

[Homebrew] - это пакетный менеджер для macOS который помогает вам легко установить PHP и различные расширения. Главный репозиторий Homebrew предоставляет "formulae" формулы для PHP 5.6, 7.0, 7.1, 7.2, 7.3, 7.4, 8.0 и PHP 8.1. Установите последнюю версию командой:

```
brew install php@8.1
```

Вы можете переключаться между Homebrew PHP вырсиями изменяя переменную `PATH`. Альтернативно, вы можете использовать [brew-php-switcher][brew-php-switcher] для переключения PHP версий автоматически.

Также вы можете переключаться вручную переключаться между PHP версиями отсоединяяя и присоединяя желаемую версию:

```
brew unlink php
brew link --overwrite php@8.0
```

```
brew unlink php
brew link --overwrite php@8.1
```

### Установка PHP через Macports

Проект [MacPorts] - это инициатива open-source сообщества по разработке
легкой в использовании системы для компиляции, установки, и обновления, так-же
командная строка, X11 или Aqua open-source программного обеспечения в операционной
системе OS X.

MacPorts supports pre-compiled binaries, so you don't need to recompile every
dependency from the source tarball files, it saves your life if you don't
have any package installed on your system.

At this point, you can install `php54`, `php55`, `php56`, `php70`, `php71`, `php72`, `php73`, `php74`, `php80` or `php81` using the `port install` command, for example:

    sudo port install php74
    sudo port install php81

And you can run `select` command to switch your active PHP:

    sudo port select --set php php81

### Install PHP via phpbrew

[phpbrew] is a tool for installing and managing multiple PHP versions. This can be really useful if two different
applications/projects require different versions of PHP, and you are not using virtual machines.

### Install PHP via Liip's binary installer

Another popular option is [php-osx.liip.ch] which provides one liner installation methods for versions 5.3 through 7.3.
It doesn't overwrite the PHP binaries installed by Apple, but installs everything in a separate location (/usr/local/php5).

### Compile from Source

Another option that gives you control over the version of PHP you install, is to [compile it yourself][mac-compile].
In that case be sure to have installed either [Xcode][xcode-gcc-substitution] or Apple's substitute
["Command Line Tools for XCode"] downloadable from Apple's Mac Developer Center.

### All-in-One Installers

The solutions listed above mainly handle PHP itself, and do not supply things like [Apache][apache], [Nginx][nginx] or a SQL server.
"All-in-one" solutions such as [MAMP][mamp-downloads] and [XAMPP][xampp] will install these other bits of software for
you and tie them all together, but ease of setup comes with a trade-off of flexibility.

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

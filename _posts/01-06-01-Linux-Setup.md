---
title: Linux Установка
isChild: true
anchor: linux_setup
---

## Linux Установка {#linux_setup_title}

Большинство GNU/Linux дистрибутивов идут в составе с PHP доступным из официальных репозиториев, но эти пакеты обычно немного отстают от
текущей стабильной версии. Есть несколько способов получить последние версии PHP в этих дистрибутивах. Например в Ubuntu или базирующихся на Debian GNU/Linux дистрибутивах,
лучшей альтернативой родным пакетам являются предоставляемые и поддерживаемые [Ondřej Surý][Ondrej Sury Blog], через его персональный архив пакетов (PPA) в Ubuntu
и DPA/bikeshed в Debian. Инструкции для каждого из них вы найдете ниже. При этом вы всегда можете использовать контейнеры, скомпилировать исходный код PHP и т. д.

### Дистрибутивы на базе Ubuntu

Для Ubuntu дистрибутивов, [PPA by Ondřej Surý][Ondrej Sury PPA] предоставляет поддерживаемые версии PHP вместе со многими расширениями PECL. Для добавления этого PPA в вашу систему, проделайте в терминале следующие шаги:

1. Сначала добавьте PPA в источники программного обеспечения вашей системы с помощью команды:

   ```bash
   sudo add-apt-repository ppa:ondrej/php
   ```

2. После добавления PPA обновите список пакетов вашей системы.:

   ```bash
   sudo apt update
   ```

Это гарантирует, что ваша система сможет получить доступ и установить последние пакеты PHP, доступные в PPA.

Вы можете переключаться между версиями PHP изменяя вашу переменную `PATH`. Как альтернативу
вы можете использовать [deb-sphp][deb-sphp] для автоматического переключения версии PHP.

Так же вы можете вручную переключаться между версиями PHP с помощью `update-alternatives` на нужную версию:

```bash
sudo update-alternatives --set php /usr/bin/php8.2
sudo update-alternatives --set phar /usr/bin/phar8.2
sudo update-alternatives --set phar.phar /usr/bin/phar.phar8.2
```

#### Дистрибутивы на базе Debian

Для дистрибутивов основанных на Debian, Ondřej Surý также [bikeshed][bikeshed] (Debian эквивалент PPA). Добавьте bikeshed в вашу ситему и обновите, следуя этим шагам:

1. Убедитесь что имеете root доступ. Если нет то возможно потребуется использование `sudo` для выполнения следующих команд.

2. Обновите ваш список системных пакетов:

   ```bash
   sudo apt-get update
   ```

3. Установите `lsb-release`, `ca-certificates`, и `curl`:

   ```bash
   sudo apt-get -y install lsb-release ca-certificates curl
   ```

4. Загрузите ключ подписи для репозитория:

   ```bash
   sudo curl -sSLo /usr/share/keyrings/deb.sury.org-php.gpg https://packages.sury.org/php/apt.gpg
   ```

5. Добавьте репозиторий в источники программного обеспечения вашей системы:

   ```bash
   sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/deb.sury.org-php.gpg] https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
   ```

6. Наконец, еще раз обновите список пакетов вашей системы:

   ```bash
   sudo apt-get update
   ```

Выполнив эти шаги, ваша система сможет установить последние версии PHP-пакетов из bikeshed.

[Ondrej Sury Blog]: https://deb.sury.org/
[Ondrej Sury PPA]: https://launchpad.net/~ondrej/+archive/ubuntu/php
[bikeshed]: https://packages.sury.org/php/
[deb-sphp]: https://github.com/nazares/deb-sphp

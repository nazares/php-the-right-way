# Contributing to PHP The Right Way

Нравится [PHP The Right Way](http://phptherightway.com) и хотите принять участие?
Замечательно! Есть много способов помочь.

Пожалуйста, найдите время, чтобы просмотреть этот документ, чтобы сделать процесс
внесения вклада простым и эффективным для всех участников.

Следование этим рекомендациям помогает показать, что вы уважаете время разработчиков,
управляющих и разрабатывающих этот проект с открытым исходным кодом. В свою очередь,
они должны ответить взаимностью на решение вашей проблемы или оценку исправлений
и функций.

## Использование issue tracker

[issue tracker](https://github.com/codeguy/php-the-right-way/issues) является
предпочтительным каналом для внесения изменений: орфографические ошибки, изменения
формулировок, новый контент и вообще [отправка запросов на включение](#pull-requests),
но, пожалуйста, соблюдайте следующие ограничения:

* Пожалуйста, **не** используйте средство отслеживания проблем для личных запросов
в службу поддержки (используйте [Stack Overflow](http://stackoverflow.com/questions/tagged/php) или IRC).

* Пожалуйста, **не** срывайте и не троллите проблемы. Держите дискуссию по теме
и уважайте мнение других.

## Pull Requests

Запросы Pull requests — отличный способ добавить новый контент в PHP «Правильно»,
а также обновить любые проблемы с браузером или другие изменения стиля.
Практически любые изменения принимаются, если они рассматриваются как конструктивные.

Соблюдение следующего процесса — лучший способ включить вашу работу в проект:

1. [Fork](http://help.github.com/fork-a-repo/) проект, клонируйте свой форк и
настройте пульты:

   ```bash
   # Clone your fork of the repo into the current directory
   git clone https://github.com/<your-username>/php-the-right-way.git
   # Navigate to the newly cloned directory
   cd php-the-right-way
   # Assign the original repo to a remote called "upstream"
   git remote add upstream https://github.com/codeguy/php-the-right-way.git
   ```

2. If you cloned a while ago, get the latest changes from upstream:

   ```bash
   git checkout gh-pages
   git pull upstream gh-pages
   ```

3. Создайте новую ветку темы (вне основной ветки разработки проекта), чтобы
содержать ваши изменения или исправления:

   ```bash
   git checkout -b <topic-branch-name>
   ```

4. Установить [Jekyll](https://github.com/jekyll/jekyll/) gem и зависимости для локального предварительного просмотра:

    ```bash
    # Install the needed gems through Bundler
    bundle install --path vendor/bundle
    # Run the local server
    bundle exec jekyll serve
    ```

5. Зафиксируйте изменения логическими фрагментами. Пожалуйста, придерживайтесь этих [git commit
   message guidelines](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
   или ваш контент вряд ли будет объединен с основным проектом. Используйте Git
   [interactive rebase](https://help.github.com/articles/about-git-rebase/)
   функции, чтобы привести в порядок ваши коммиты, прежде чем публиковать их.

6. Локально объедините (или перебазируйте) вышестоящую ветку разработки в вашу тематическую ветку:

   ```bash
   git pull [--rebase] upstream gh-pages
   ```

7. Push свою ветку темы к вашей вилке:

   ```bash
   git push origin <topic-branch-name>
   ```

8. [Open a Pull Request](https://help.github.com/articles/using-pull-requests/)
    с понятным названием и описанием.

## Соглашение о вкладе и использование

Отправляя pull request в этот репозиторий, вы соглашаетесь разрешить владельцам проекта лицензировать вашу работу в
соответствии с условиями [Creative Commons Attribution-NonCommercial-ShareAlike
3.0 Unported License](http://creativecommons.org/licenses/by-nc-sa/3.0/).

Один и тот же контент и лицензия будут использоваться для всех публикаций PHP The Right Way, включая, помимо прочего:

* [phptherightway.com](http://phptherightway.com)
* Переводы phptherightway.com
* [LeanPub: PHP The Right Way](https://leanpub.com/phptherightway/)
* Переводы "LeanPub: PHP The Right Way"

Весь контент теперь полностью бесплатен и всегда будет таким.

## Руководство по стилю для авторов

1. Используйте американскую английскую орфографию (*только основной английский репозиторий*)
2. Используйте четыре (4) пробела для отступа текста; не используйте вкладки
3. Оберните весь текст до 120 символов.
4. Примеры кода должны соответствовать PSR-1 или выше.
5. Используйте [GitHub Flavored Markdown](https://github.github.com/gfm/) для всего контента.
6. Используйте URL-адреса, не зависящие от языка, при обращении к внешним веб-сайтам, таким как руководство [php.net](http://php.net/urlhowto.php).

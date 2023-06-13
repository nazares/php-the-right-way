---
isChild: true
title: Скомпилированные шаблоны
anchor:  compiled_templates
---

## Скомпилированные шаблоны {#compiled_templates_title}

Хотя PHP превратился в зрелый объектно-ориентированный язык, он [не сильно улучшился][article_templating_engines] как
язык шаблонов. Скомпилированные шаблоны, такие как [Twig], [Brainy] или [Smarty]*, заполняют этот пробел, предлагая
новый синтаксис, специально предназначенный для создания шаблонов. От автоматического экранирования до наследования и
упрощенных структур управления — скомпилированные шаблоны разработаны так, чтобы их было проще писать, чище читать и
безопаснее использовать. Скомпилированные шаблоны можно даже использовать на разных языках, [Mustache] является хорошим
примером этого. Поскольку эти шаблоны должны быть скомпилированы, производительность снижается незначительно, однако при
правильном кэшировании это минимально.

**Хотя Smarty предлагает автоматическое экранирование, эта функция НЕ включена по умолчанию.*

### Простой пример скомпилированного шаблона

Использование библиотеки [Twig].

{% highlight html+jinja %}
{% raw %}
{% include 'header.html' with {'title': 'User Profile'} %}

<h1>User Profile</h1>
<p>Hello, {{ name }}</p>

{% include 'footer.html' %}
{% endraw %}
{% endhighlight %}

### Пример скомпилированных шаблонов с использованием наследования

Использование библиотеки [Twig].

{% highlight html+jinja %}
{% raw %}
// template.html

<html>
<head>
    <title>{% block title %}{% endblock %}</title>
</head>
<body>

<main>
    {% block content %}{% endblock %}
</main>

</body>
</html>
{% endraw %}
{% endhighlight %}

{% highlight html+jinja %}
{% raw %}
// user_profile.html

{% extends "template.html" %}

{% block title %}User Profile{% endblock %}
{% block content %}
    <h1>User Profile</h1>
    <p>Hello, {{ name }}</p>
{% endblock %}
{% endraw %}
{% endhighlight %}

[article_templating_engines]: http://fabien.potencier.org/templating-engines-in-php.html
[Twig]: https://twig.symfony.com/
[Brainy]: https://github.com/box/brainy
[Smarty]: https://www.smarty.net/
[Mustache]: https://mustache.github.io/

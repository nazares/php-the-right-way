---
title: Простые PHP-шаблоны
isChild: true
anchor:  plain_php_templates
---

## Простые PHP-шаблоны {#plain_php_templates_title}

Простые шаблоны PHP — это просто шаблоны, в которых используется собственный код PHP. Это естественный выбор, поскольку
PHP сам по себе является языком шаблонов. Это просто означает, что вы можете комбинировать PHP-код с другим кодом,
например HTML. Это выгодно для PHP-разработчиков, так как нет необходимости изучать новый синтаксис, они знают доступные
им функции, а их редакторы кода уже имеют встроенную подсветку синтаксиса PHP и автодополнение. Кроме того, простые
шаблоны PHP, как правило, работают очень быстро, так как не требуют этапа компиляции.

Каждый современный PHP-фреймворк использует какую-то систему шаблонов, большинство из которых по умолчанию использует
простой PHP. Вне фреймворков такие библиотеки, как [Plates][plates] или [Aura.View][aura], упрощают работу с простыми
шаблонами PHP, предлагая современные функции шаблонов, такие как наследование, макеты и расширения.

### Простой пример обычного PHP-шаблона

Использование библиотеки [Plates][plates].

```php
<?php // user_profile.php ?>

<?php $this->insert('header', ['title' => 'User Profile']) ?>

<h1>User Profile</h1>
<p>Hello, <?=$this->escape($name)?></p>

<?php $this->insert('footer') ?>
```

### Пример простых шаблонов PHP с использованием наследования

Использование библиотеки [Plates][plates].

```php
<?php // template.php ?>

<html>
<head>
    <title><?=$title?></title>
</head>
<body>

<main>
    <?=$this->section('content')?>
</main>

</body>
</html>
```

```php
<?php // user_profile.php ?>

<?php $this->layout('template', ['title' => 'User Profile']) ?>

<h1>User Profile</h1>
<p>Hello, <?=$this->escape($name)?></p>
```

[plates]: https://platesphp.com/
[aura]: https://github.com/auraphp/Aura.View

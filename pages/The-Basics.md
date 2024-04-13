---
layout: page
title:  Основы
sitemap: true
---

# Основы

## Операторы сравнения

Операторы сравнения — часто упускаемый из виду аспект PHP, который может привести ко многим неожиданным результатам.
Одна из таких проблем возникает из-за строгих сравнений (сравнение логических значений как целых чисел).

```php
<?php
$a = 5;   // 5 as an integer

var_dump($a == 5);       // compare value; return true
var_dump($a == '5');     // compare value (ignore type); return true
var_dump($a === 5);      // compare type/value (integer vs. integer); return true
var_dump($a === '5');    // compare type/value (integer vs. string); return false

//Equality comparisons
if (strpos('testing', 'test')) {    // 'test' is found at position 0, which is interpreted as the boolean 'false'
    // code...
}

// vs. strict comparisons
if (strpos('testing', 'test') !== false) {    // true, as strict comparison was made (0 !== false)
    // code...
}
```

* [Операторы сравнения](https://www.php.net/language.operators.comparison)
* [Таблица сравнения](https://www.php.net/types.comparisons)
* [Шпаргалка по сравнению](https://phpcheatsheets.com/index.php?page=compare)

## Условные операторы

### Оператор If

При использовании операторов 'if/else' внутри функции или метода класса существует распространенное заблуждение, что необходимо использовать оператор 'else'.
в сочетании с объявлением потенциальных результатов. Однако, если результат должен определить возвращаемое значение, 'else' не является
необходимым, поскольку 'return' завершит функцию, в результате чего 'else' станет спорным.

```php
<?php
function test($a)
{
    if ($a) {
        return true;
    } else {
        return false;
    }
}

// vs.

function test($a)
{
    if ($a) {
        return true;
    }
    return false;    // else is not necessary
}

// or even shorter:

function test($a)
{
    return (bool) $a;
}
```

* [Оператор If](https://www.php.net/control-structures.if)

### Оператор Switch

Операторы Switch — отличный способ избежать набора бесконечных if и elseif, но есть несколько вещей, о которых следует знать:

* Операторы switch сравнивают только значения, а не тип (эквивалент '==')
* Они перебирают каждый случай, пока не будет найдено совпадение. Если совпадение не найдено, используется значение по умолчанию (если оно определено).
* Без 'break' они будут продолжать реализовывать каждый случай до достижения break/return.
* Within a function, using 'return' alleviates the need for 'break' as it ends the function
* Bспользование 'return' внутри функции устраняет необходимость в 'break', поскольку оно завершает функцию.

```php
<?php
$answer = test(2);    // the code from both 'case 2' and 'case 3' will be implemented

function test($a)
{
    switch ($a) {
        case 1:
            // code...
            break;             // break is used to end the switch statement
        case 2:
            // code...         // with no break, comparison will continue to 'case 3'
        case 3:
            // code...
            return $result;    // within a function, 'return' will end the function
        default:
            // code...
            return $error;
    }
}
```

* [Оператор Switch](https://www.php.net/control-structures.switch)
* [PHP switch](http://phpswitch.com/)

## Глобальное пространство имен

При использовании пространства имен вы можете обнаружить, что внутренние функции скрыты от функций написанных вами. Чтобы исправить это, обратитесь к
глобальной функции, используя обратную косую черту перед именем функции.

```php
<?php
namespace phptherightway;

function fopen()
{
    $file = \fopen();    // Our function name is the same as an internal function.
                         // Execute the function from the global space by adding '\'.
}

function array()
{
    $iterator = new \ArrayIterator();    // ArrayIterator is an internal class. Using its name without a backslash
                                         // will attempt to resolve it within your namespace.
}
```

* [Глобальное пространство](https://www.php.net/language.namespaces.global)
* [Глобальные правила](https://www.php.net/userlandnaming.rules)

## Строки

### Конкатенация

* Если длина вашей строки превышает рекомендуемую (120 символов), рассмотрите возможность объединения строк.
* Для удобства чтения лучше использовать операторы конкатенации, а не операторы присваивания.
* Находясь в исходной области действия переменной, отступ при конкатенации использует новую строку.

```php
<?php
$a  = 'Multi-line example';    // concatenating assignment operator (.=)
$a .= "\n";
$a .= 'of what not to do';

// vs

$a = 'Multi-line example'      // concatenation operator (.)
    . "\n"                     // indenting new lines
    . 'of what to do';
```

* [Строковые операторы](https://www.php.net/language.operators.string)

### Типы строк

Строки — это последовательность символов, которая должна звучать довольно просто. Тем не менее, существует несколько различных типов
строки, и они предлагают немного другой синтаксис и немного другое поведение.

#### Одинарные кавычки

Одинарные кавычки используются для обозначения 'литеральной строки'. Литеральные строки не пытаются анализировать специальные символы или
переменные.

Если вы используете одинарные кавычки, вы можете ввести имя переменной в строку, например: `'some $thing'`, и вы увидите
точный вывод `some $thing`. При использовании двойных кавычек будет предпринята попытка оценить имя переменной `$thing` и показать
ошибки, если переменная не найдена.

```php
<?php
echo 'This is my string, look at how pretty it is.';    // no need to parse a simple string

/**
 * Output:
 *
 * This is my string, look at how pretty it is.
 */
```

* [Одинрные кавычки](https://www.php.net/language.types.string#language.types.string.syntax.single)

#### Двойные кавычки

Двойные кавычки — это швейцарский армейский нож для строк. Они будут анализировать не только переменные, как упоминалось выше, но и все виды
специальных символов, например `\n` для новой строки, `\t` для табуляции и т. д.

```php
<?php
echo 'phptherightway is ' . $adjective . '.'     // a single quotes example that uses multiple concatenating for
    . "\n"                                       // variables and escaped string
    . 'I love learning' . $code . '!';

// vs

echo "phptherightway is $adjective.\n I love learning $code!"  // Instead of multiple concatenating, double quotes
                                                               // enables us to use a parsable string
```

Двойные кавычки могут содержать переменные; это называется «интерполяция».

```php
<?php
$juice = 'plum';
echo "I like $juice juice";    // Output: I like plum juice
```

При использовании интерполяции часто бывает, что переменная касается другого символа. Это приведет
к некоторой путанице относительно того, как называется переменная и что такое буквальный символ.

Чтобы решить эту проблему, заключите переменную в пару фигурных скобок.

```php
<?php
$juice = 'plum';
echo "I drank some juice made of $juices";    // $juice cannot be parsed

// vs

$juice = 'plum';
echo "I drank some juice made of {$juice}s";    // $juice will be parsed

/**
 * Complex variables will also be parsed within curly brackets
 */

$juice = array('apple', 'orange', 'plum');
echo "I drank some juice made of {$juice[1]}s";   // $juice[1] will be parsed
```

* [Двойные кавычки](https://www.php.net/language.types.string#language.types.string.syntax.double)

#### Nowdoc синтаксис

Синтаксис Nowdoc был представлен в версии 5.3 и внутренне ведет себя так же, как одинарные кавычки, за исключением того, что он подходит для
использование многострочных строк без необходимости объединения.

```php
<?php
$str = <<<'EOD'             // initialized by <<<
Example of string
spanning multiple lines
using nowdoc syntax.
$a does not parse.
EOD;                        // closing 'EOD' must be on it's own line, and to the left most point

/**
 * Output:
 *
 * Example of string
 * spanning multiple lines
 * using nowdoc syntax.
 * $a does not parse.
 */
```

* [Nowdoc синтаксис](https://www.php.net/language.types.string#language.types.string.syntax.nowdoc)

#### Heredoc синтаксис

Синтаксис Heredoc внутренне ведет себя так же, как и двойные кавычки, за исключением того, что он подходит для использования многострочных символов.
строки без необходимости объединения.

```php
<?php
$a = 'Variables';

$str = <<<EOD               // initialized by <<<
Example of string
spanning multiple lines
using heredoc syntax.
$a are parsed.
EOD;                        // closing 'EOD' must be on it's own line, and to the left most point

/**
 * Output:
 *
 * Example of string
 * spanning multiple lines
 * using heredoc syntax.
 * Variables are parsed.
 */
```

* [Heredoc синтаксис](https://www.php.net/language.types.string#language.types.string.syntax.heredoc)

> Следует отметить, что многострочные строки также могут быть сформированы путем продолжения их по нескольким строкам в операторе. _например._

```php
$str = "
Example of string
spanning multiple lines
using statement syntax.
$a are parsed.
";

/**
 * Output:
 *
 * Example of string
 * spanning multiple lines
 * using statement syntax.
 * Variables are parsed.
 */
```

### Что быстрее?

Существует миф о том, что строки с одинарными кавычками работают немного быстрее, чем строки с двойными кавычками. Это в корне не верно.

Если вы определяете одну строку и не пытаетесь объединить значения или что-то сложное, то либо одна
или строка в двойных кавычках будет полностью идентична. Ни один из них не быстрее.

Если вы объединяете несколько строк любого типа или интерполируете значения в строку с двойными кавычками, то
результаты могут различаться. Если вы работаете с небольшим количеством значений, конкатенация происходит на мгновение быстрее. С большим количеством
значения, интерполяция происходит на мгновение быстрее.

Независимо от того, что вы делаете со строками, ни один из типов никогда не окажет заметного влияния на работу вашего приложения.
Попытка переписать код для использования того или иного варианта всегда бесполезна, поэтому избегайте подобных микро-оптимизаций, если вы действительно не понимаете значение и влияние различий.

* [Опровержение мифа об эффективности одинарных кавычек](https://www.npopov.com/2012/01/09/Disproving-the-Single-Quotes-Performance-Myth.html)

## Тернарные операторы

Тернарные операторы — отличный способ сократить код, но их часто используют чрезмерно. Хотя тернарные операторы могут быть
сложенные/вложенные, для удобства чтения рекомендуется использовать по одному на строку.

```php
<?php
$a = 5;
echo ($a == 5) ? 'yay' : 'nay';
```

Для сравнения, вот пример, в котором читабельность приносится в жертву ради уменьшения количества строк.

```php
<?php
echo ($a) ? ($a == 5) ? 'yay' : 'nay' : ($b == 10) ? 'excessive' : ':(';    // excess nesting, sacrificing readability
```

Чтобы 'вернуть' значение с помощью тернарных операторов, используйте правильный синтаксис.

```php
<?php
$a = 5;
echo ($a == 5) ? return true : return false;    // this example will output an error

// vs

$a = 5;
return ($a == 5) ? 'yay' : 'nope';    // this example will return 'yay'

```

Следует отметить, что вам не нужно использовать тернарный оператор для возврата логического значения. Примером этого
могло бы быть.

```php
<?php
$a = 3;
return ($a == 3) ? true : false; // Will return true if $a == 3 or false

// vs

$a = 3;
return $a == 3; // Will return true if $a == 3 or false

```

Это также можно сказать для всех операций (===, !==, !=, == и т. д.).

#### Использование скобок с тернарными операторами для обозначения формы и функции

При использовании тернарного оператора скобки могут сыграть свою роль в улучшении читаемости кода, а также для включения объединений
внутри блоков утверждений. Пример того, когда нет необходимости использовать скобки:

```php
<?php
$a = 3;
return ($a == 3) ? "yay" : "nope"; // return yay if $a == 3 or nope

// vs

$a = 3;
return $a == 3 ? "yay" : "nope"; // return yay if $a == 3 or nope
```

Обьединение в скобки также дает нам возможность создавать объединения внутри блока операторов, где блок будет проверяться
в целом. Например, этот пример ниже, который вернет true, если оба ($a == 3 и $b == 4) верны, а $c == 5 —
тоже верно.

```php
<?php
return ($a == 3 && $b == 4) && $c == 5;
```

Другой пример — приведенный ниже фрагмент, который вернет true, если ($a != 3 И $b != 4) ИЛИ $c == 5.

```php
<?php
return ($a != 3 && $b != 4) || $c == 5;
```

Начиная с PHP 5.3, можно исключить среднюю часть тернарного оператора.
Выражение "expr1 ?: expr3" возвращает expr1, если expr1 имеет значение TRUE, и expr3 в противном случае.

* [Тернарные операторы](https://www.php.net/language.operators.comparison)

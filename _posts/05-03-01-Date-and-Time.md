---
title:   Дата и время
isChild: true
anchor:  date_and_time
---

## Дата и время {#date_and_time_title}

В PHP есть класс DateTime, который поможет вам при чтении, записи, сравнении или вычислении даты и времени. Помимо
DateTime, в PHP есть много функций, связанных с датой и временем, но он предоставляет хороший объектно-ориентированный
интерфейс для наиболее распространенных применений. DateTime может обрабатывать часовые пояса, но это выходит за рамки
этого краткого введения.

Чтобы начать работу с DateTime, преобразуйте необработанную строку даты и времени в объект с помощью фабричного метода
createFromFormat() или выполните команду new DateTime, чтобы получить текущую дату и время. Используйте метод `format()`,
чтобы преобразовать DateTime обратно в строку для вывода.

{% highlight php %}
<?php
$raw = '22. 11. 1968';
$start = DateTime::createFromFormat('d. m. Y', $raw);

echo 'Start date: ' . $start->format('Y-m-d') . PHP_EOL;
{% endhighlight %}

Вычисление с помощью DateTime возможно с классом DateInterval. DateTime имеет такие методы, как `add()` и `sub()`,
которые принимают DateInterval в качестве аргумента. Не пишите код, который ожидает одинаковое количество секунд каждый
день. И переход на летнее время, и изменение часового пояса нарушат это предположение. Вместо этого используйте интервалы
дат. Для вычисления разницы дат используйте метод `diff()`. Он вернет новый DateInterval, который очень легко отобразить.

{% highlight php %}
<?php
// create a copy of $start and add one month and 6 days
$end = clone $start;
$end->add(new DateInterval('P1M6D'));

$diff = $end->diff($start);
echo 'Difference: ' . $diff->format('%m month, %d days (total: %a days)') . PHP_EOL;
// Difference: 1 month, 6 days (total: 37 days)
{% endhighlight %}

Вы можете использовать стандартные сравнения объектов DateTime:

{% highlight php %}
<?php
if ($start < $end) {
    echo "Start is before the end!" . PHP_EOL;}
{% endhighlight %}

Последний пример для демонстрации класса DatePeriod. Он используется для повторения повторяющихся событий. Он может
принимать два объекта DateTime, начало и конец, а также интервал, в течение которого он будет возвращать все промежуточные
события.

{% highlight php %}
<?php
// output all thursdays between $start and $end
$periodInterval = DateInterval::createFromDateString('first thursday');
$periodIterator = new DatePeriod($start, $periodInterval, $end, DatePeriod::EXCLUDE_START_DATE);
foreach ($periodIterator as $date) {
    // output each date in the period
    echo $date->format('Y-m-d') . ' ';
}
{% endhighlight %}

Популярным расширением PHP API является [Carbon](https://carbon.nesbot.com/). Он наследует все в классе DateTime, поэтому
требует минимальных изменений кода, но дополнительные функции включают поддержку локализации, дополнительные способы
добавления, вычитания и форматирования объекта DateTime, а также средства для тестирования вашего кода путем имитации даты
и времени по вашему выбору.

*[Читать о DateTime][datetime]
*[Читать о форматировании даты][dateformat] (принятые параметры строки формата даты)

[datetime]: https://secure.php.net/book.datetime
[dateformat]: https://secure.php.net/function.date

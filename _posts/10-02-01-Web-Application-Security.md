---
isChild: true
title: Безопасность Веб-приложения
anchor:  web_application_security
---

## Безопасность Веб-приложения {#web_application_security_title}

Очень важно для каждого разработчика PHP изучить [основы безопасности веб-приложений][4],
которые можно разбить на несколько широких тем:

1. Разделение кода и данных.
   * Когда данные выполняются как код, вы получаете SQL-инъекцию, межсайтовый скриптинг, включение локальных/удаленных файлов и т. д.
   * Когда код печатается в виде данных, вы получаете утечку информации (раскрытие исходного кода или, в случае программ на C, достаточно информации, чтобы обойти [ASLR][5]).
2. Логика приложения.
   * Отсутствуют элементы управления аутентификацией или авторизацией.
   * Проверка ввода.
3. Рабочая среда.
   * Версии PHP.
   * Сторонние библиотеки.
   * Операционная система.
4. Криптографические недостатки.
   * [Weak random numbers][6].
   * [Chosen-ciphertext attacks][7].
   * [Side-channel information leaks][8].

Есть плохие люди, готовые и желающие использовать ваше веб-приложение. Важно, чтобы вы приняли необходимые меры
предосторожности для повышения безопасности вашего веб-приложения. К счастью, замечательные люди из [The Open Web
Application Security Project][1] (OWASP) составили исчерпывающий список известных проблем с безопасностью и способы защиты
от них. Это необходимо прочитать разработчику, заботящемуся о безопасности. [Survive The Deep End: PHP Security][3]
Padraic Brady — еще одно хорошее руководство по безопасности веб-приложений для PHP.

* [Читать OWASP Security Guide][2]

[1]: https://www.owasp.org/
[2]: https://www.owasp.org/index.php/Guide_Table_of_Contents
[3]: https://phpsecurity.readthedocs.io/en/latest/index.html
[4]: https://paragonie.com/blog/2015/08/gentle-introduction-application-security
[5]: http://searchsecurity.techtarget.com/definition/address-space-layout-randomization-ASLR
[6]: https://paragonie.com/blog/2016/01/on-design-and-implementation-stealth-backdoor-for-web-applications
[7]: https://paragonie.com/blog/2015/05/using-encryption-and-authentication-correctly
[8]: https://blog.ircmaxell.com/2014/11/its-all-about-time.html

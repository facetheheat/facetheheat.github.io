---
layout: post
title: Tweetbot for Mac
date: '2015-07-20 18:34:08'
tags:
- Mac
---

Получилось так, что я вновь вернулся к использованию твиттера.
Причин как всегда много, но сейчас совсем не про прокрастинацию.

Приятно пользоваться качественными программами. Я начал вести этот микроблог с [описания всего софта](http://pavel.miroshnichen.co/2015/01/17/setup-2015/), которым я пользуюсь с особым удовольствием. Вот и сейчас решил не откладывать, а воспользоваться ценой со скидкой и купить [Tweetbot for Mac](https://geo.itunes.apple.com/ru/app/tweetbot-for-twitter/id557168941?mt=12&uo=4&at=1001l9qh&ct=blog). Что уже говорить, про `Tweetbot` ходит много легенд :)

>Про Tweetbot ходит много легенд

## Простой покупкой я не отделаюсь
Привычка же остается - вбивать в адрес баре `twitter.com`. В `Safari` я привык переходить по адресам через хоткей `⌘+L`. Как от этого избавиться радикально? Один из способов - использовать `Little Snitch`.

Создаем правило - добавляем правило для `Safari.app`:

![](http://pavel.miroshnichen.co/images/2015/07/Screen-Shot-2015-07-20-at-21-03-19.png){: .center-image .responsive-image }

## Переход по ссылкам
После блокировки по домену остается вопрос - как преходить по ссылкам?

Соберем `Safari Extension`, который использует `URL Scheme` и откроет твиттер-ссылку в `Tweetbot`. Я нагуглил первый вариант и он мне подошел. Что делать:

* `Safari -> Develop -> Show Extension Builder`;
* по [ссылке](http://robmathers.github.io/tweetbotlinks/) скачиваем * `.tar.gz` или `*.zip`;
* распаковываем и перетаскиваем папку `TweetbotLinks.safariextension` в окно `Safari Extension Builder`;
* `Build package`, сохраняем пакет для следующего раза;
* `Install package`.

![](http://pavel.miroshnichen.co/images/2015/07/Screen-Shot-2015-07-20-at-21-11-57-1.png){: .center-image .responsive-image }


Все!   
Теперь при клике на твиттер ссылку она будет открываться в `Tweetbot`!

## ⌘ 

Подписывайтесь на [@previewthenew](https://twitter.com/previewthenew) , не стесняйтесь.

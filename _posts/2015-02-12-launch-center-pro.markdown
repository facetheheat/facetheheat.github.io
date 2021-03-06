---
layout: post
title: Как настроить Launch Center Pro
date: '2015-02-12 09:03:00'
redirect_from: "/2015/02/13/launch-center-pro/"
summary: 'Launch Center Pro - лаунчер приложений для iOS c поддержкой виджетов и URL-schemes'
tags:
- iOS
- Автоматизация
---

Консервативный подход в работе iOS всем нам очень нравится. Мы используем с удовольствием(или нет?) док, рабочие столы, папки, выезжающие центр уведомлений или пункт управления. Чего только стоит переключение между приложениями, на iPad можно даже задействовать жесты.

В App Store находится множество приложений, упрощающих доступ или использование телефона. Проще говоря, делают все, чтобы повысить наши с вами удобство, производительность и удовольствие. К счастью для нас, про большинство из них мы даже не слышали и не представляем о чем идет речь, что от нас хотят.
За нас уже все решили и нам это нравится, а если не нравится - идем за Android.

Сегодня я расскажу про одно такое приложение. Называется [Launch Center Pro](https://geo.itunes.apple.com/ru/app/launch-center-pro-shortcut/id532016360?mt=8&at=1001l9qh&ct=blog) - лаунчер для iOS. Что же это такое?
Лаунчер - приложение, которое создано упросить запуск всех остальных программ.  По своим функциям это аналог панели управления на iOS (выдвигается снизу), когда в два движения включается фонарик, калькулятор, камера или секундомер.

![](http://pavel.miroshnichen.co/images/2015/02/lcp-wide-small.jpg)


## Как использовать Launch Center Pro
Launch Center Pro - это приложение, созданное для быстрого запуска других приложений или выполнения каких-либо действий.

Это полноценная автоматизация своей работы на iOS. Вы значительно сократите время на набор номера, звонок, написание письма,
поиск в интернете или закладка любимого сайта, отправку твита, прокладку маршрута до дома или работы и многое другое.

![](http://pavel.miroshnichen.co/images/2015/02/demo-small-2.gif)
![](http://pavel.miroshnichen.co/images/2015/02/lcp-dock.jpg)

Я не сторонник установки сторонних приложений, но Launch Center Pro мне понравился:
> скоростью работы,
> удобством,
> гибкостью настроек,
> интуитивным интерфейсом.

Остановлюсь подробнее на первых двух.

**Скорость работы** - первое, на что мы обращаем внимание, пусть и в фоне. Для лаунчера это важнейший показатель для выживания, иначе его моментально отправят в корзину. Работа приложения Launch Center Pro удивляет своей скоростью, даже на моем старичке iPhone 5S (на самом деле это сарказм). После тапа по иконке приложения можно приступать ко всем остальным действиям. Работа приложения после запуска остается такой же высокой.

**UX.** Удивительно, но во всем хорошем найдется ложка дегтя. Так и в iOS для меня это оказались папки или Stacks. Меня раздражает группировать приложения в паки только потому, что в папку нужно заходить(один тап) и из папки нужно выходить(еще одни тап). Это доводит до бешенства. А вот в Launch Center Pro не нужно заходить в папку в буквальном смысле, достаточно свайпом(передвинуть на нее палец) открыть содержание папки. Если палец убрать - папка закроется автоматически. После 2 минут использования обычные папки на iOS я стал еще больше ненавидеть :)



## Здравствуй, Launch Center Pro

Приложение дополняет основные функции телефона.

1. Приложения из панели управления не добавляем в лаунчер;
2. Часто используемые группы переношу вниз экрана;
3. Нижний ряд оставляю пустым, как правило, над ним находится палец.

Отдельно стоит упомянуть про группы. На первом экране у меня они все разбиты по группам(папкам).
Вложенные иконки в группах расположены в определенном порядке:
большой палец левой и правой рук не должен перекрывать ничего.



## Скриншоты
![](http://pavel.miroshnichen.co/images/2015/02/LCP-04-copy.jpg)
![](http://pavel.miroshnichen.co/images/2015/02/LCP-03-copy.jpg)
![](http://pavel.miroshnichen.co/images/2015/02/LCP-02-copy.jpg)
![](http://pavel.miroshnichen.co/images/2015/02/LCP-01-copy.jpg)

## Добавляем приложения в Launch Center Pro
К сожалению, приложений которые поддерживаются в Launch Center Pro не так много.
Полный список представлен на [странице приложения](http://actions.contrast.co/all).

Как же добавить остальные приложения в Launch Center Pro?
Рассказываю. Все приложения в LCP работают через URL Scheme. Что это такое?
Например, вызвав из любого приложения ссылку tel:+15551234567 iOS распознает, что такая ссылка открывается приложением Телефон.app и предложит набрать номер. Разработчики LCP добавляют поддержку приложений, но добавить абсолютно всё невозможно. Мы самостоятельно пропишем ссылку для всех наших приложений. Да, придется установить произвольные значки,
но это лучше, чем совсем ничего.

#### Как узнать URL Scheme для приложения?
1. Скачиваем приложение на Mac'е в iTunes.
2. Переименовываем расширение файла из ***.ipa** в ***.zip**.
3. Распаковываем архив.
4. Открываем **plist** файл `Папка/Payload/Application.apps/Info.plist`
5. Ищем строки URL Schemes, копируем значение и вставляем в Launch Center Pro.

В этом случае мы не сможем узнать параметров, которые можно передать в приложение. Но уже простой запуск приложения - это полдела.

##### Примеры
*Яндекс.Карты, открыть карту и построить маршрут*
`yandexmaps://build_route_on_map?lat_to=XXXXXX&lon_to=YYYYYY`
*где XXXXXX - latitude
и YYYYYY - longitude
Этот URL позволяет в одно движение(свайп) проложить маршрут до дома или работы. Очень удобный способ для тех, кто за рулем.*

*Яндекс.Навигатор, принимает те же параметры, что и Яндекс.Карты*
`yandexnavi:build_route_on_map?lat_to=XXXXXX&lon_to=YYYYYY`

*Яндекс.Транспорт, Яндекс.Метро*
```
yandextransport:
yandexmetro:
```
*Telegram Messenger, открыть мессенджер и написать сообщение определенному контакту*
`telegram://msg?text=Hello&to=+ZXXXYYYYYYY`

*Дзен-мани, Qiwi Visa Wallet, Megafon, FitPort*
```
zenmoney-ru:
qiwi:
megafonlk:
fitport:
```

*Hyperlapse, Pro Camera*
```
hyperlapse://camera
procamera:
```

*Deezer, SoundHound*
```
deezer:
soundhound:
```

*Сообщения, Viber, Skype, Find My Friends*
```
sms:+XYYYZZZZZZZ
viber:
skype:
findmyfriends:
```


## ⌘

Я почти не рассказал о возможностях [Launch Center Pro для iPhone](https://geo.itunes.apple.com/ru/app/launch-center-pro-shortcut/id532016360?mt=8&at=1001l9qh&ct=blog), я только изучаю данный продукт.
Основная функциональность - запуск приложений. Ниже представлены ссылки на ресурсы, где можно подробнее прочитать про использования LCP, возможно, почерпнёте для себя что-то интересное.

Официальная документация
http://contrast.co/launch-center-pro/
http://help.contrast.co/hc/en-us/categories/200048556-Launch-Center-Pro

Много интересного на MacStories
- [http://www.macstories.net/tutorials/launch-center-pro-2-3-1-for-power-users/](http://www.macstories.net/tutorials/launch-center-pro-2-3-1-for-power-users/)
- [http://www.macstories.net/reviews/launch-center-pro-2-0-review/](http://www.macstories.net/reviews/launch-center-pro-2-0-review/)
- [http://www.macstories.net/reviews/launch-center-pro-2-3-extends-ios-automation/](http://www.macstories.net/reviews/launch-center-pro-2-3-extends-ios-automation/)
- [http://www.macstories.net/reviews/based-on-launch-center-pro-contact-center-simplifies-contact-shortcuts/](http://www.macstories.net/reviews/based-on-launch-center-pro-contact-center-simplifies-contact-shortcuts/)
- [http://www.macstories.net/tutorials/launch-center-pro-guide/](http://www.macstories.net/tutorials/launch-center-pro-guide/)
- [http://www.macstories.net/tutorials/spotify-actions-for-launch-center-pro/](http://www.macstories.net/tutorials/spotify-actions-for-launch-center-pro/)
- [http://www.macstories.net/roundups/my-launch-center-pro-setup/](http://www.macstories.net/roundups/my-launch-center-pro-setup/)
- [http://www.macstories.net/tutorials/redeeming-app-store-promo-codes-with-launch-center-pro/](http://www.macstories.net/tutorials/redeeming-app-store-promo-codes-with-launch-center-pro/)

## P.S
Есть чем поделиться? Оставляйте в комментариях свои интересные workflow для автоматизации на iOS.

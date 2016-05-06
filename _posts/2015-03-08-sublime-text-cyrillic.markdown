---
layout: post
title: Sublime Text и кириллица
date: '2015-03-08 16:24:35'
tags:
- Mac
---

Мне очень нравится текстовый редактор Sublime Text, но иногда я сталкиваюсь с необычными ошибками в скриптах, написанных в нем.
На самом деле ошибки простые, но вот визуально их тяжело быстро обнаружить. Перейду от слов к делу.


# На примере Shell-скрипта

{% highlight bash lineanchors %}
# example.sh
echo "converting CoreStorage Volume ..."
echo "diskutil cs сonvert /Volumes/CORESTORAGE"
diskutil cs сonvert /Volumes/CORESTORAGE
echo "...done"
{% endhighlight %}

На первый взгляд ошибок нет. Но при выполнении в консоли появляется сообщение:
{% highlight bash lineanchors %}
diskutil: did not recognize coreStorage verb "сonvert";
type "diskutil coreStorage" for a list
{% endhighlight %}

Из названия заметки можно догадаться, что ошибка в слове "**c**onvert", где вместо "c" латинской написана "с" кириллическая.

В терминале можно проверить командой
{% highlight bash lineanchors %}
echo "diskutil cs сonvert" |hexdump -c
{% endhighlight %}

![](http://pavel.miroshnichen.co/images/2015/03/Screen-Shot-2015-03-08-at-19-01-26.png)

Первый символ в слове convert отличается от остальных, ошибка найдена.

# А в чем проблема Sublime Text?
А вот как это выгдядит в Sublime Text

![](http://pavel.miroshnichen.co/images/2015/03/Screen-Shot-2015-03-08-at-18-52-29.png)

За собственные ошибки мы платим. Предлагаю свести их к минимуму. Задача - обнаружить такие ошибки на этапе написания скрипта, чтобы во время отладки не отвлекаться на подобные, досадные опечатки.

Самый простой вариант - сохранять файл с кодировкой Ansi - Western (Windows 1252), но при сохранении Sublime ругается, что файл не может быть сохранен, т.к. содержит несовместимые символы. Но вот какие именно? Вариант отпадает.

Второй способ - найти/написать плагин с подсветкой таких ошибок. Я нашел первый попавшийся хайлайтер, доработал и забыл про проблему.

# Highlighter (cyrillic edition)

Настройка плагина:

1. Установим плагин [Highlighter](https://packagecontrol.io/packages/Highlighter).
2. Откроем настройки `Sublime Text -> Preferences -> Package Settings -> Highlighter -> Settings - User`
3. Внесем изменения в шаблон поиска, изменим значение highlighter_regex

{% highlight bash lineanchors %}
"highlighter_regex": "((?<=[a-zA-Z])[А-Яа-я])|([А-Яа-я](?=[a-zA-Z]))"
{% endhighlight %}

# I'm lovin it
![](http://pavel.miroshnichen.co/images/2015/03/Screen-Shot-2015-03-08-at-18-53-13.png)

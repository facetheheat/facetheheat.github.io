---
layout: post
title: "Настраиваем Hazel - автоматизатор для Mac"
date: 2015-11-11 11:13:05
tags:
- Mac
- Автоматизация
- Продуктивность
---

Приложение [Hazel](https://www.noodlesoft.com/hazel.php) - первый шаг к автоматизации в OS X. Организация хранения файлов, автоматическая сортировка, рутинная работа над файлами - ежедневные задачи для Hazel. Мощное приложение Hazel не очевидно в настройке, я сделал подборку своих фундаментальных правил. 

## Правило №1: Рабочий стол
Любые файлы или папки с рабочего стола переносятся в `~/Downloads`.  
Рабочий стол всегда чист.
![](http://pavel.miroshnichen.co/images/2015/11/hazel-01.png){: .center-image .responsive-image }


## Правило №2: Удаление приложений
При удалении программ Hazel будет отслеживать и предлагать удалять зависимые файлы (настройки, временные файлы и т.п.).
![](http://pavel.miroshnichen.co/images/2015/11/hazel-02.png){: .center-image .responsive-image }
 
## Правила для Downloads

**Правило №3:** Перенос .torrent файлов  
Сохраненные *.torrent файлы перемещаются в `~/Downloads/TORRENTS/`.  
Не всегда требуется открывать Transmission, поэтому отслеживание *.torrent файлов в определенной директории для Transmission отключено.
![](http://pavel.miroshnichen.co/images/2015/11/hazel-03.png){: .center-image .responsive-image }


**Правило №4:** Конвертация книг для Kindle  
Файл с расширением *.fb2 будет автоматически сконвертирован через `fb2mobi` в формат mobi. Можно пойти дальше и настроить отправку книг через Send-to-Kindle по электронной почте.
![](http://pavel.miroshnichen.co/images/2015/11/hazel-04.png){: .center-image .responsive-image }

![Embedded Script](/images/2015/11/hazel-05.png){: .center-image .responsive-image }

## Правила для Screen Shot'ов
Cохранение скриншотов настроено на `~/Documents/Screen Shots/`.
{% highlight bash lineanchors %}
defaults write com.apple.screencapture location "~/Documents/Screen Shots"
killall SystemUIServer
{% endhighlight %}


**Правило №5:** Переименовывает скриншоты в «Screen Shot», снятые под разными локализациями («Screen Shot», «Снимок экрана» и т.п.). 
![](http://pavel.miroshnichen.co/images/2015/11/hazel-06.png){: .center-image .responsive-image }

**Правило №6:** Hazel переносит устаревшие скриншоты (старше 50 дней) в подпапку c именем `~/Documents/Screen Shots/ГГГГ`.
![](http://pavel.miroshnichen.co/images/2015/11/hazel-07.png){: .center-image .responsive-image }


## Правила для отсканированных документов
При сохранении сканов с iOS я добавляю к имени тип документа: «чек», «покупка», «поездка» и т.п. Сканы сохраняются в папку «Документы/Загрузки».

**Правило №7:** Hazel сортирует в подпапки по типам документов. Например, файл с текстом «чек» переносит в «Документы/Покупки».
![](http://pavel.miroshnichen.co/images/2015/11/hazel-08.png){: .center-image .responsive-image }

## Правила для рабочих документов
**Правило №8:** Перенос рабочих файлов из Downloads в Documents/WORK. Файлы сохраненные с рабочего домена domain.com перемещаются в `~/Documents/WORK/INBOX`.  

Посмотреть `Source URL/Address` можно командой `$ mdls filename`

![](http://pavel.miroshnichen.co/images/2015/11/hazel-09.png){: .center-image .responsive-image }


**Правило №9:** Сортировка рабочих документов по типам файлов. Документы(doc,xls,pdf,txt,md и т.п) перемещаются в «WORK/Docs»;
Программы перемещаются из «WORK/INBOX» в «WORK/DMGs».
В зависимости от задач можно упростить для себя структурирование.

**Правило №10:** Hazel автоматически отмонтирует образ с определенным именем, если образ был замонтирован более 10 минут назад. 

Мне приходится часто работать с разными приложениями, через некоторое время забываешь какая версия примонтирована. 

Hazel заставляет монтировать нужный образ повторно, чтобы быть уверенным в нужной версии.
![](http://pavel.miroshnichen.co/images/2015/11/hazel-10.png){: .center-image .responsive-image }


# Похожие статьи
[«Освобождаем место на SSD при помощи Dropbox, Hazel и Python»](http://pavel.miroshnichen.co/2015/02/02/hazel-ios-apps/).

# ⌘
Если появились вопросы и предложения отвечайте в комментариях.  
Приятно встречать единомышленников.




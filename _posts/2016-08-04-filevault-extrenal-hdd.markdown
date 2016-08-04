---
layout: post
title: 'Как включить шифрование Filevault 2 для внешних дисков'
date: '2016-08-04 10:10:18'
tags:
- Mac
---

Полное шифрование диска позволяет предотвратить несанкционированный доступ к личным данным. После перехода на Mac Mini я включил шифрование с помощью функции FileVault только для системного диска. Фотографии и медиатеки хранятся на внешнем 2Тб диске, расскажу как быстро защитить внешний диск без потери данных.


## Включение шифрования на системном диске
В macOS шифрование загрузочного диска включается одним кликом и перезагрузкой. Подробная инструкция доступна на сайте Apple [«Использование FileVault для шифрования загрузочного диска на компьютере Mac»](https://support.apple.com/ru-ru/HT204837).

![](/images/2016/08/Screen%20Shot%202016-07-04%20at%209.39.22.png)


## Включение шифрования FileVault для внешних дисков
Если мы говорим про чистый диск или диск с данными, которые не нужны, то можно отформатировать диск с шифрованием через `Disk Utility`. 

Мой 2Тб диск был забит данными на половину, пришлось конвертировать диск через cli версию `diskutil`. Что нам потребуется:

- диск с таблицей GPT (GUID Partition Table). Если диск с MBR, необходимо сконвертировать его в GPT;
- создадим на диске логическую группу CosreStorage;
- включим шифрование для логического раздела из группы CoreStorage;
- дождёмся завершения зашифровки данных.

Все операции будут проходить над разделом `/Volumes/BLACK`

#### Конвертация GPT диска в логическую группу CoreStorage

Полный список документированных операций можно получить командой `diskutil CoreStorage`.

Конвертация GPT диска в Core Storage Logical Volume
{% highlight bash %}
$ diskutil cs convert /Volumes/BLACK

Started CoreStorage operation on disk2s2 BLACK
Resizing disk to fit Core Storage headers
Creating Core Storage Logical Volume Group
Attempting to unmount disk2s2
Switching disk2s2 to Core Storage
Core Storage LVG UUID: 939C2993-0427-4341-A25E-800E7A237BE9
Core Storage PV UUID: FC676F1C-570A-4263-91A1-E6C59C8AB64D
Core Storage LV UUID: 1D1AEEDF-2794-4459-9D1A-D7E328B726BF
Finished CoreStorage operation on disk2s2 BLACK
{% endhighlight %}

Проверяем статус операции:
{% highlight bash %}
$ diskutil cs list 
...
+-- Logical Volume Group 939C2993-0427-4341-A25E-800E7A237BE9
=========================================================
Name:         BLACK
Status:       Offline
Size:         0 B (0 B)
Free Space:   -none-
|
+-< Physical Volume FC676F1C-570A-4263-91A1-E6C59C8AB64D
------------------------------------------------
Index:    0
Disk:     disk2s2
Status:   Checking
Size:     2000021315584 B (2.0 TB)
{% endhighlight %}

Для продолжения необходимо переподключить диск. Для проверки статуса я указал идентификатор логической группы Logical Volume Group. LVG статус перейдёт в Online.

{% highlight bash %}
$ diskutil cs info 939C2993-0427-4341-A25E-800E7A237BE9  

Core Storage Properties:
   Role:                       Logical Volume Group (LVG)
   UUID:                       939C2993-0427-4341-A25E-800E7A237BE9
   LVG Name:                   BLACK
   LVG Version:                1
   LVG Size:                   2000021315584 B
   LVG Free Space:             18964480 B
   LVG Status:                 Online
   LVG Sparse:                 No
   Fusion Drive:               No
{% endhighlight %}

На диске включена логическая группа, всё готово к включению шифрования на заданных разделах. Получить идентификатор раздела можно следующим образом:

{% highlight bash %}
$ diskutil cs list
...
   |
    +-> Logical Volume Family 6B00786D-BE89-4932-9795-6EBEDC381935
        ----------------------------------------------------------
        Encryption Type:         None
        |
        +-> Logical Volume 1D1AEEDF-2794-4459-9D1A-D7E328B726BF
            ---------------------------------------------------
            Disk:                  disk4
            Status:                Online
            Size (Total):          1999650029568 B (2.0 TB)
            Revertible:            Yes (no decryption required)
            LV Name:               BLACK
            Volume Name:           BLACK
            Content Hint:          Apple_HFS
{% endhighlight %}

Проверяем размер тома и метку `LV Name: BLACK`. Включаем шифрование для логического тома, у меня это `Logical Volume 1D1AEEDF-2794-4459-9D1A-D7E328B726BF`. Терминал запросит указать пароль, предлагаю сразу записать его в 1Password.

{% highlight bash %}
$ diskutil cs encryptVolume 1D1AEEDF-2794-4459-9D1A-D7E328B726BF

New passphrase for existing volume:
Confirm new passphrase:
The Core Storage Logical Volume UUID is 1D1AEEDF-2794-4459-9D1A-D7E328B726BF
Started CoreStorage operation on disk4 BLACK
Scheduling encryption of Core Storage Logical Volume
Core Storage LV UUID: 1D1AEEDF-2794-4459-9D1A-D7E328B726BF
Finished CoreStorage operation on disk4 BLACK
{% endhighlight %}

Проверяем статус операции командой `diskutil cs info LVID`
{% highlight bash %}
$ diskutil cs info 1D1AEEDF-2794-4459-9D1A-D7E328B726BF      10:37

Core Storage Properties:
   Role:                       Logical Volume (LV)
   UUID:                       1D1AEEDF-2794-4459-9D1A-D7E328B726BF
   Parent LVF UUID:            6B00786D-BE89-4932-9795-6EBEDC381935
   Parent LVG UUID:            939C2993-0427-4341-A25E-800E7A237BE9
   Device Identifier:          disk4
   LV Status:                  Online
   Conversion State:           Converting
   LV Bytes Converted:         1943634182144 B
   LV Conversion Progress:     97%
   Content Hint:               Apple_HFS
   LV Name:                    BLACK
   Volume Name:                BLACK
   LV Size:                    1999650029568 B
mac@MacMini ~/Downloads $                          20:51
{% endhighlight %}

Скорость включения шифрования зависит от объёма занятых данных на диске. Мой 2Тб диск забит на половину, включение шифрования заняло 21 час:

- 11 часов = 44% [23:22 - 10:17]
- 21 час = 97%  [10:17 - 20:51]

{% highlight bash %}
$ diskutil cs info 1D1AEEDF-2794-4459-9D1A-D7E328B726BF    21:09
...
Conversion State:           Complete
...
LV Conversion Progress:     100%
{% endhighlight %}

{% highlight bash %}
$ diskutil cs list
...
+-> Logical Volume Family 6B00786D-BE89-4932-9795-6EBEDC381935
------------------------------------------------------
Encryption Type:         AES-XTS
Encryption Status:       Unlocked
Conversion Status:       Complete
High Level Queries:      Fully Secure
{% endhighlight %}

После завершения операции переподключаем диск, проверяем, что пароль подошёл и диск замонтировался.

![](/images/2016/08/Screen%20Shot%202016-07-16%20at%209.45.09.png)

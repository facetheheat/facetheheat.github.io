---
layout: post
title: 'Как решить проблемы с Wi-Fi на macOS 10.12 Sierra'
date: '2016-10-16 16:10:58'
description: 'Решение проблем с Wi-Fi на последней версии macOS 10.12 Sierra. Если в браузерах перестают открываться страницы, решение проблемы читайте в этой заметке.'
tags:
- Mac
---

Я в первый раз столкнулся с проблемами в Wi-Fi при использовании macOS. Хотя знаю, что в предыдущих версиях macOS уже были похожие проблемы. 

## Оборудование:
- Airport Extreme 2.4Ghz/5Ghz,
- Mac Mini с macOS 10.12 Sierra,
- MacBook Pro с macOS 10.12 Sierra.

## Проблема: 
- В браузерах на маках не открываются сайты. 
На iPhone и iPad все отлично, как и на windows ноутбуке жены. 

![](/images/2016/10/network-diagnostics.png)

Если открыть сетевые настойки `System Preferences -> Network -> Assist Me...` и запустить Network Diagnostics, то браузер начинает работать какое-то время. Чаще всего 2-3 минуты, затем проблема повторяется.

## Решение:  
1) Отключить Wi-Fi.  
2) Перейти в папку `/Library/Preferences/SystemConfiguration/`.  
3) Удалить файлы:  
{% highlight bash %}
com.apple.airport.preferences.plist
com.apple.network.eapolclient.configuration.plist
com.apple.wifi.message-tracer.plist
NetworkInterfaces.plist
preferences.plist
{% endhighlight %}
4) Перезагрузить мак с macOS 10.12 Sierra.  
5) Включить Wi-Fi.  

На данный момент проблема ушла, в Safari и Chrome сайты открываются моментально.


---
layout: post
title:  "Jenkins - инструмент для непрерывной интеграции"
date:   2013-10-26 8:45:11
categories: ci, jenkins
---
Официальный сайт: [http://jenkins-ci.org/](http://jenkins-ci.org/)

## Установка:

{% highlight bash %}
wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-get install jenkins
{% endhighlight %}

После установки Jenkins запустится и будет слушать соединения на порту 8080, для того чтобы изменить порт, следует отредактировать в файле `/etc/default/jenkins` переменную HTTP_PORT (и другие переменные при необходимости) Рестартуем Jenkins и готово. Теперь можно заходить на `localhost:8080` (по умолчанию) и видеть работающий Jenkins.

## Настройка сборки проекта:
 - Создаем новое задание
 - Указываем репозиторий из которого необходимо забрать код
 - Указываем переодичность запуска
 - Указываем дополнительно запускаемые скрипты

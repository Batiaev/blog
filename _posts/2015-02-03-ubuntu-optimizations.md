---
layout: post
title:  "Ubuntu optimizations"
date:   2015-02-03 21:19:11
categories: linux optimization ubuntu
---

[http://help.ubuntu.ru/wiki/ubuntu_optimization](http://help.ubuntu.ru/wiki/ubuntu_optimization)

##Swappiness
Процент занятой оперативной памяти после которого начнется использование swap

Значение по умолчанию 60

Изменить на 10 (при занятой на 90% озу начнется использование swap)

{% highlight bash %}
sudo nano /etc/sysctl.conf

vm.swappiness=10
{% endhighlight %}

##Cache popular apps

{% highlight bash %}
sudo apt-get install preload

sudo touch /var/lib/preload/preload.state
sudo chmod 600 /var/lib/preload/preload.state
sudo /etc/init.d/preload restart
{% endhighlight %}

###Config files

`sudo gedit /etc/preload.conf`

###Log files

`sudo tail -n 100 /var/log/preload.log`

##Clean apt cache
Время от времени стоит чистить кэш APT. Для этого воспользуйтесь данной командой:

{% highlight bash %}
sudo apt-get autoclean
sudo apt-get autoremove
{% endhighlight %}

##Disable GRUB menu
Когда ваша Ubuntu загружается, то по умолчанию на 10 секунд появляется меню GRUB. Предлагаю отключить его. Для этого воспользуйтесь данной командой:

`sudo nano /etc/default/grub`
`GRUB_TIMEOUT=0`

##Caching symbol tables
Создайте пустой каталог

`mkdir ~/.compose-cache`

Ваши Qt/GTK программы будут чуток быстрее стартовать и потреблять меньше памяти, благодаря тому, что libX11 будет создавать в ~/.compose-cache кеши распарсенной информации и использовать ее повторно.

##Speedup Unity

Установите, если не установлен `compizconfig-settings-manager`.
Запустите Менеджер настройки CompizConfig (Сompiz Configuration Settings Manager - ccsm) и перейдите в OpenGL Plugin, в котором отключите Синхронизировать с VBlank.
Перейдите в Composite и отключите Определить частоту обновления.
Отключите в разделе Эффекты плагины Анимация (Animations) и/или Проявление/исчезание окон.
Если не используете сенсорные устройства, то отключите плагин Unity MT Grab Handles.
В Общие - Общие настройки выставьте Задержка отклика в 2000.

##Optimize FS mounting
в /etc/fstab добавляем опции "noatime,nodiratime",

##Use all processor cores
Если у вас многоядерный процессор, то стоит настроить Ubuntu так, чтобы при загрузке были задействованы все ядра. Для этого введите данную команду:
`sudo nano /etc/init.d/rc`

После чего найдите следующую строчку:

`CONCURRENCY=none`

И замените её на такую:
`CONCURRENCY=shell`

##Use TmpFS

На раздел /tmp приходится очень много операций чтения/записи, поэтому рекомендуется перенести его в оперативную память (если, конечно, у вас её достаточно). Для этого откройте файл /etc/fstab:

`sudo nano /etc/fstab`

И добавьте такую строчку в конец файла:
`tmpfs /tmp tmpfs defaults,noexec,nosuid 0 0`

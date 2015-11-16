---
layout: post
title:  "Crib on SSH"
date:   2015-01-09 19:25:11
categories: ssh linux terminal
---

Пост является сжатой выдержкой необходимой мне информации из [поста на хабре](http://habrahabr.ru/post/122445/) автора [amarao](http://habrahabr.ru/users/amarao/).

*SSH* (англ. *Secure Shell* — «безопасная оболочка») — сетевой протокол прикладного уровня, позволяющий производить удалённое управление операционной системой и туннелирование TCP-соединений (например, для передачи файлов). Схож по функциональности с протоколами Telnet и rlogin, но, в отличие от них, шифрует весь трафик, включая и передаваемые пароли. SSH допускает выбор различных алгоритмов шифрования. SSH-клиенты и SSH-серверы доступны для большинства сетевых операционных систем.

## Управление ключами
- `ssh-keygen` - Создание ключа
- `ssh-copy-id user@serve` - Копирование ключа на сервер
- `~/.ssh/known_hosts` - Список известных ключей в файле
- `ssh-keygen -R server` - Удаление известного ключа сервера
- `ssh-keygen -R 127.0.0.1` - Удаление ключа IP

## Копирование файлов
`scp path/myfile user@8.8.8.8:/full/path/to/new/location/`
Либо:
`scp user@8.8.8.8:/full/path/to/file /path/to/put/here`

- `scp -r -P2222 path/myfile user@8.8.8.8:/full/path/to/new/location/` - Использование нестандартного порта [-P2222] и рекурсивного копирования всей папки[-r]
- `sshfs desunote.ru:/var/www/website.ru/ /media/website.ru -o reconnect` - Удалённая файловая система (sshfs)
- `fusermount -u /path` - Отмонтировать
- `sudo umount -f /path` - Отмонтировать при залипании соединения
- `ssh user@server ls /etc/ ` - Удалённое исполнение кода
- `ssh user@server -t remove_command` - Для приложений с управляющим терминалом

## Алиасы и опции по умолчанию
Файл `~/.ssh/config`
или `/etc/ssh/ssh_config`

Содержимое файла:
{% highlight bash %}
Host hostname
	Hostname    app1.host.com
	User        username
	ForwardX11    yes
	Compression    yes

Host *
	User username
	Compression yes
{% endhighlight %}

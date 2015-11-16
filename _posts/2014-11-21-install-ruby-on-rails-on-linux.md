---
layout: post
title:  "Install Ruby on Rails on linux"
date:   2014-11-21 22:09:11
categories: linux RoR ruby
---

Официальный сайт языка Ruby: [https://www.ruby-lang.org/ru/](https://www.ruby-lang.org/ru/)

Официальный сайт фреймворка Ruby on Rails: [http://rubyonrails.org/](http://rubyonrails.org/)

*Ruby* - это динамический, рефлективный, интерпретируемый высокоуровневый язык программирования для быстрого и удобного объектно-ориентированного программирования. Язык обладает независимой от операционной системы реализацией многопоточности, строгой динамической типизацией, сборщиком мусора и многими другими возможностями. Ruby близок по особенностям синтаксиса к языкам `Perl` и `Eiffel`, по объектно-ориентированному подходу — к `Smalltalk`.

Создателем языка является *Юкихиро Мацумото* (яп. `松本行弘`, чаще яп. `まつもとゆきひろ`, также известный как `Matz`, род. 14 апреля 1965) — японский разработчик свободного ПО.

*Ruby on Rails* — фреймворк, написанный на языке программирования `Ruby`. Ruby on Rails предоставляет архитектурный образец `Model-View-Controller` (модель-представление-контроллер) для веб-приложений, а также обеспечивает их интеграцию с веб-сервером и сервером базы данных.

Кроссплатформенная реализация интерпретатора языка Ruby является полностью свободной. И выпускается под лицензией [GNU GPL v2](http://opensource.org/licenses/GPL-2.0).

*Ruby on Rails* является открытым программным обеспечением и распространяется под [лицензией MIT](http://opensource.org/licenses/MIT).


## Установка Ruby on Rails.

- `sudo apt-get update` - Обновляем пакеты
- `sudo apt-get install curl` - Устанавливаем curl
- `sudo apt-get install ruby-bundler` - Устанавливаем bundler
- `curl -L get.rvm.io | bash -s stable` - Устанавливаем *RVM* (**Ruby Version Manager**). Это программа позволяющая использовать несколько версий Ruby на одной машине.
- `source ~/.rvm/scripts/rvm` - Запускаем RVM
- `rvm requirements` - Устанавливаем зависимости необходимые RVM:
- `rvm install 2.2.1` - Установка Ruby
- `rvm use 2.2.1 --default` - Поскольку мы используем RVM — необходимо указать какую версию использовать:
- `rvm rubygems current` - Установка RubyGems
- `gem install rails` - Установка Rails
- `sudo apt-get install nodejs` - Для корректной работы RoR необходим node.js.


Этапы создания своего первого приложения на Ruby on Rails:
- Создаем директорию в которой будут храниться приложения RoR и переходим в нее.
{% highlight bash %}
$ mkdir ~/ruby_on_rails/
$ cd ~/ruby_on_rails/
{% endhighlight %}
- Создаем дефолтную структуру приложения
    $ rails first_app
- Запускаем встроенные простой веб сервер названный WEBrick
    $ ./first_app/script/server
- Готово! Переходим по адресу: `localhost:3000` и видим дефолтную страницу Ruby on Rails.

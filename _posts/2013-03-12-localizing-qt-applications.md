---
layout: post
title:  "Локализация приложений написанных на Qt"
date:   2013-03-12 21:51:21
categories: C++ L10n Qt IT
---
Официальный сайт: http://qt-project.org/

- Добавляем в *.pro файл следующий блок:
{% highlight make %}
	TRANSLATIONS += appName.ru_RU.ts
{% endhighlight %}

Где appName - имя проекта (совпадает с названием *.pro файла)
В данном примере добавлен файла перевода на русский язык.

- Выполняем из терминала:

{% highlight bash %}
$ lupdate appName.pro
{% endhighlight %}

После этого будут созданы файлы перевода указанные в *.pro файле .

- Заполняем переводы через программу Qt 4 Linguist
Выполняем из терминала:

{% highlight bash %}
$ lrelease -compress name.ru_RU.ts -qm name.ru_RU.qm
{% endhighlight %}

Из заполненных файлов перевода *.ts будут собраны бинарные файлы локализации *.qm.

 - Добавляем файлы перевода в файл ресурсов чтобы после компиляции он был вшит в бинарный файл.

Для этого если файл ресурсов еще не был создан создаем его и добавляем в его в *.pro файл.

	RESOURCES += res.qrc

После этого открываем его из Qt Creator и добавляем файл перевода при помощи кнопки Add Files
Затем в файл main.cpp прописываем следующий код:

{% highlight c++ %}
QTranslator tr, qt_tr;
// Загрузка перевода файла ресурсов (ему был добавлен алиас lang_ru_RU)
tr.load(":/lang_ru_RU");
// Из исходников Qt достаем файл локализации Qt (окна about и т.п.)
qt_tr.load(":/qt_ru_RU");
// Установливаем перевода для нашего приложения
app.installTranslator(&tr);
app.installTranslator(&qt_tr);
{% endhighlight c++ %}
---
layout: post
title:  "Пример приложения на Gtk+ c использованием Glade"
date:   2013-04-07 19:48:21
categories: cairo, C++, Glade, Gtk+, libcairomm, libgtkmm, IT  
---
Официальный сайт: https://glade.gnome.org/

Для быстрого создания графического интерфейса для вашего приложения написанного с использованием GTK+ можно воспользоваться утилитой Glade.

В зависимости от используемой версии GTK+ необходимо устанавливать разные версии Glade.

Для создания интерфейса на GTK+ v2 необходимо установить версию Glade 3.8.0:

`# aptitude install glade-gtk2`

Для использования GTK+ v3 неоходимо установить версию Glade 3.12.1:

`# aptitude install glade`

Перед этим разумеется необходимо установить пакет deb-пакет самого GTK+

Для второй версии : `# aptitude install libgtk2.0-dev`

Для третьей версии : `# aptitude install libgtk-3-dev`

Так как GTK+ написан на С, если вы пишете на C++ можно использовать обертку на С++ - библиотеку gtkmm.
Так же соответственно вторая : `# aptitude install libgtkmm-3.0-dev`
И треться версии: `# aptitude install libgtkmm-2.4-dev`

Для рендеринга 2D графики можно использовать как библиотеку на С :

`# aptitude install libcairo-2.0-dev`

Так и её С++ обертку:

`# aptitude install libcairomm-1.0-dev`

После того как мы создали в Glade интерфейс, его необходимо подключить к приложению. Рассмотрим простое приложение с использованием библиотеки GTK+ и интерфеса созданного через Glade.

// Подключаем библиотеки для работы с cairo и gtk+
{% highlight c++ %}
#include <cairo.h>
#include <gtk/gtk.h>

// обработчик сигнала копки
static void helloworld (GtkButton *button, gpointer label)
{
    // установаем метке текст
    gtk_label_set_text(GTK_LABEL(label), "Привет, Gtk!");
}  

// создание окна мы вынесли в отдельную функцию
static GtkWidget* create_window()
{
    // Здесь будем хранить ошибки
    GError* error = NULL;

    // билдер окна, здесь загружаем файл с интерфейсом, созданным в Glade
    GtkBuilder *builder = gtk_builder_new ();
    if (!gtk_builder_add_from_file (builder, "exampleGui.ui", &error))
    {
        // обрабатываем ситуацию когда загрузить файл не удалось
        g_critical ("Cannot load file: %s", error->message);
        g_error_free (error);
    }


    // получаем из интерфейса кнопку и лейбл
    GtkButton *button = GTK_BUTTON(gtk_builder_get_object(builder, "button1"));
    GtkLabel *label = GTK_LABEL(gtk_builder_get_object(builder, "label1"));
    // коннектим сигнал нажатия кнопки (cliked) к вызову функции helloworld
    g_signal_connect(GTK_BUTTON(button), "clicked", G_CALLBACK(helloworld), label);

    // получаем виджет окна, чтобы его показать
    GtkWidget *window = GTK_WIDGET(gtk_builder_get_object (builder, "window1"));
    if (!window)
    {
        g_critical ("Error cannot get window");
    }
    g_object_unref (builder);

    return window;
}

int main (int argc, char *argv[])
{
    // запускаем GTK+
    gtk_init (&argc, &argv);

    // вызываем нашу функцию для создания окна
    gtk_widget_show (create_window ());

    // передаём управление GTK+
    gtk_main ();
    return 0;
}
{% endhighlight %}


Особенности компиляции:
Компилятору и линкеру дополнительной опцией необходимо будет скормить результат выполнения следующей команды:
(компилятору соответственно --cflags, а линкеру --libs)

В случае gtkmm2 : `pkg-config --cflags --libs gtkmm-2.4`

Для gtkmm3 : `pkg-config --cflags --libs gtkmm-3.0`

Для cairomm : `pkg-config --cflags --libs cairomm-1.0`

Для gtk2 : `pkg-config --cflags --libs gtk+-2.0`

Для gtk3 : `pkg-config --cflags --libs gtk+-3.0`

Чтобы он подцепил все необходимые для сборки библиотеки. 
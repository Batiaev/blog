---
layout: post
title:  "Crib on svn"
date:   2014-01-04 16:45:11
categories: vcs svn
---
Официальный сайт: [http://subversion.apache.org/](http://subversion.apache.org/)

## Основные команды:

 - Извлекаем файлы проекта из репозитория:
`svn checkout http://repository.url/svn/name # сокращение svn co`

 - Получаем обновления из репозитория:
`svn update # сокращение svn up`

 - Извлекаем ревизию файла с номером rev_num:
`svn update -r rev_num ./file_name`

 - Добавляем файл в репозиторий:
`svn add ./file_name`

 - Коммитим файл в репозиторий:
`svn commit ./file_name`

 - Переименовываем файл в репозитории:
`svn rename ./old_file_name ./new_file_name`

 - Удаляем файл/директорию из репозитория:
`svn remove ./file_name`

 - Просматриваем локально измененные файлы:
`svn status # сокращение: svn st`

 - Просматриваем локально измененные и изменившиеся в репозитории файлы:
`svn status -u # сокращение: svn st -u`

 - Показывает локальные изменения в файле построчно:
`svn diff ./file_name`

 - Показывает различия между ревизией rev_num1 и rev_num2 файла:
`svn diff -r rev_num1:rev_num2 ./file_name`

 - Откатывает локальные изменения файла (выгружает из репозитория последнюю закоммиченную ревизию):
`svn revert ./file_name`

 - Откатывает все локальные изменения файлов:
`svn revert -R ./`

 - Список ревизий с комментариями:
`svn log ./file_name`

 - Показывает авторов изменений файла построчно:
`svn blame ./file_name # синоним: svn annotate`

 - Добавляем файл в список игнорируемых файлов:
`svn propset svn:ignore ./file_name .`

 - Установка атрибутов файла:
`svn propset svn:keywords "Id Author Date" ./file_name`

 - Снимает блокировки с файлов:
`svn cleanup`

 - Снять блокировку файла (URL можно узнать с помощью команды svn info ./file_name | grep URL, его и нужно передавать в svn unlock):
`svn unlock http://repository.url/svn/file_name`

 - Заменяет текстовое описание коммита, где rev_num — номер ревизии, commit_text_file — путь к файлу, содержащему новый комментарий к коммиту:
`svnadmin setlog --bypass-hooks /path/to/repository -r rev_num ./commit_text_file`

 - Выводит помощь по команде command_name, например, «svn help update»:
`svn help command_name`

 - Откатываем ревизию номер rev_to_rollback до ревизии rev_good, причем все изменения старше rev_to_rollback сохраняются (Например, у файла есть ревизии 11,12 и 13. Хотим откатить 12-ую ревизию, но так, что бы изменения 13-ой остались в силе. Делаем тогда так: svn merge -r 12:11 ./file_name):
`svn merge -r rev_to_rollback:rev_good ./file_name`

 - Создаем ветку с названием new_branch_name из главной линии разработки:
`svn copy http://repository.url/svn/name/trunk/ http://repository.url/svn/name/branches/new_branch_name/`

- Проверяем, что будет изменено при объединении веток, где
  - rev_num1 — номер ревизии, когда ваша ветка была «открыта», или это м.б. номер предыдущего объединения (слияния),
  - rev_num2 — версия главной линии разработки, с которой производим объединение.
  Необходимо отметить, что все изменения будут применены для директории, в которой выполнялась эта команда:
`svn merge --dry-run -r rev_num1:rev_num2 http://repository.url/svn/name/trunk/`

 - Синхронизирует вашу ветку с главной линией разработки с учетом ревизий:
  - rev_num1 — номер ревизии, когда ваша ветка была «открыта», или это м.б. номер предыдущего объединения (слияния),
  - rev_num2 — версия главной линии разработки, с которой производим объединение.
  Необходимо отметить, что все изменения будут применены для директории, в которой выполнялась эта команда:
`svn merge -r rev_num1:rev_num2 http://repository.url/svn/name/trunk/`
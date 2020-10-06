Использование Lua скриптов
==========
Lua скрипты из состава библиотеки позволяют работать с несколькими терминалами Quik одновременно.

Как подключиться к двум терминалам сразу
----------------------------------------

Достаточно сделать ряд простых действий:
1. Найти в файле `config.json` секцию `servers`, там будет название опции `scriptName` со значением `Quik_2`. В данном случае `Quik_2` является названием файла в папке lua (расширение `.lua` в `config.json` указывать нельзя).
2. Изменить опции согласно вашим предпочтениям. По умолчанию, дополнительный сокет сервер будет запущен на localhost'e (т.е. опции `responseHostname` и `callbackHostname` имеют значение `127.0.0.1`), а порты (опции `responsePort` и `callbackPort`) равны `34132` для сервера запросов-ответов и `34133` для сервера коллбэков (данные, которые хочет отправить Квик). Порты не должны конфликтовать с уже указанными портами в файле `config.json`
3. Добавить `Quik_2.lua` в Quik и запустить. При этом необязательно запускать `QuikSharp.lua`, если он вами не используется. Если используется и для него указаны другие порты, то, безусловно, можно запускать оба.

Все!

Вопросы и ответы
----------------

- Как добавить еще сервера?

Скопируйте файл `Quik_2.lua` и сохраните его в той же папке под другим именем, например, `MyBroker.lua`. В файле `config.json` в секции `servers` скопируйте текст внутри фигурных скобок `{"scriptName"..."responseHostname"..."responsePort"..."callbackHostname"..."callbackPort"...}`, поставьте запятую после `}`, вставьте скопированный текст и измените в нем данные. Как минимум, нужно указать в `scriptName` название файла скрипта (в примере это `MyBroker`), а в опциях портов указать любые свободные номера портов. Такую процедуру можно делать столько раз, сколько серверов вам нужно. Не забудьте, что `responsePort` и `callbackPort` не могут быть одинаковыми и повторяться в файле.

- Как обновляться на новые версии библиотеки и скриптов в частности?

В новых версиях будет меняться код скриптов и код `config.json`. Но если вы вносили изменения в `config.json`, то сохраните в другом месте файл с вашими изменениями. После этого замените все старые файлы новыми. Обратите внимание, что, возможно, в одном из обновлений содержимое `Quik_2.lua` изменится и все созданные вами лично копии этого файла потребуется пересоздать на основе обновленного файла. Продолжаем. Отредактируйте файл `config.json` в соответствии с настройками из старого файла (если не меняли ничего, делать ничего не надо). Процесс обновления завершен.

- Как сделать так, чтобы можно было подключаться к сокету из локальной сети WiFi с другого устройства?

Нужно указать в `responseHostname` и `callbackHostname` значение `0.0.0.0`. Лучше так не делать и вот, почему. Когда компьютер подключен к роутеру, то разрешение подключаться к нему извне (а именно это делает `0.0.0.0`) открывает доступ к нему всему миру при допущении, что роутер недостаточно хорошо защищен и настроен. А так как при подключении к сокетам нет ни пароля, ни шифрования, открытый доступ всему миру открывает ваш Квик всем. Т.е. если вы все же хотите подключаться из локальной сети, позаботьтесь о безопасности и верных настройках роутера.

- Можно ли переименовать `Quik_2.lua`?

Да, только укажите новое имя в `scriptName` файла `config.json`.


- Можно ли переименовать `QuikSharp.lua`?

Нет. Этот файл обязательно должен сохранить свое имя, потому что все остальные скрипты используют часть его кода.
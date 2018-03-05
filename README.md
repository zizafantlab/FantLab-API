# Fantlab-API
Публичный репозиторий по API библиографического краудсорсингового портала **fantlab.ru**.   
Предназначен для:
* документирования текущего состояния API
* взаимодействия программистов FL и пользователей API через систему *Issues*/*Pull Requests*

Предыдущая версия руководства располагается по адресу https://goo.gl/CwQfmb. Некоторая информация (например, по *OAuth*-авторизации) сюда пока не перенесена.

Предложения и замечания по работе API пишите в *Issues* данного репозитория.

## Вводная информация
1. API работает в тестовом режиме, текущая версия: **v0.9.15** (*[см.историю изменений](History.md)*). До версии **1.0** возможны большие изменения в выдачах.
2. Домен для запросов - **https://api.fantlab.ru**.
3. Возможные HTTP-коды ответов: *200* (успех), *404* (ошибка запроса).
4. Из-за особенностей серверного языка (бэкенд написан на *Perl*) в выдачах уделено мало внимания типизации данных, например, вместо числа может прийти строка (e.g. `"work_id":"1"`). Это не баг. В подобных случаях в документации указан не действительный тип поля (строка), а тот, к которому можно автоматически привести (e.g. `work_id: Int`).
5. В текстовых данных могут встретиться HTML-тэги (отсылки на сущности базы - тэг *a*). Пример: `“notes”:”Переиздание сборника рассказов <a href=\”/work320\”>Стивен Кинг «Бегущий человек»</a>”`. Полный список сущностей базы: *autor*, *art*, *dictor*, *translator*, *person*, *work*, *edition*, *series*, *publisher*, *film*, *award*, *contest*, *user*, *topic*, *article*, *blog*, *blogarticle*. Также могут встретиться и bb-тэги вида *[user]* и т.п.. По возможности от них избавляемся, но они могут до сих пор проскакивать.
6. В случае, если тип поля в документации обозначен как *null*, это означает одно из двух: либо поле может вообще отсутствовать, либо поле есть, но его значение равно *null*. Впрочем, с точки зрения конечного пользователя это одно и то же.
7. Для удобства описания были введены дополнительные типы данных: *Boolean* ("0" (false) / "1" (true)), *Date* (строка в формате `yyyy-MM-dd`), *DateTime* (строка в формате `yyyy-MM-dd HH:mm:ss`), *Url* (ссылка на файл/картинку, обычно без протокола).
8. Если какое-нибудь поле может присутствовать или быть неравным *null* только при определенном переданном параметре, то в описании типа в этом случае указан соответствующий параметр (например, `# [biblio_blocks] список произведений`). Если поле не равно *null* при любом переданном параметре, в описании типа указан параметр `[any]`.

## Содержание
1. [Поиск по библиографической базе](Docs/search.md#Поиск-по-библиографической-базе)
    * [Общий поиск](Docs/search.md#Общий-поиск)
    * [Поиск авторов](Docs/search.md#Поиск-авторов)
    * [Поиск произведений](Docs/search.md#Поиск-произведений)
    * [Поиск изданий](Docs/search.md#Поиск-изданий)
    * [Поиск книжных серий](Docs/search.md#Поиск-книжных-серий)
    * [Поиск премий](Docs/search.md#Поиск-премий)
    * [Поиск персон](Docs/search.md#Поиск-персон)
    * [Поиск издательств](Docs/search.md#Поиск-издательств)
    * [Поиск фильмов](Docs/search.md#Поиск-фильмов)
    * [Поиск статей](Docs/search.md#Поиск-статей)
2. [Автор](Docs/author.md#Автор)
    * [Список авторов](Docs/author.md#Список-авторов)
    * [Основная информация](Docs/author.md#Основная-информация)
    * [Список изданий](Docs/author.md#Список-изданий)
    * [Список наград](Docs/author.md#Список-наград-отдельно)
    * [Список отзывов](Docs/responses.md#Отзывы-на-одно-произведение)
3. [Произведение](Docs/work.md#Произведение)
    * [Основная информация](Docs/work.md#Основная-информация)
    * [Расширенная информация](Docs/work.md#Расширенная-информация)
    * [Список отзывов](Docs/responses.md#Отзывы-на-одно-произведение)
4. [Издание](Docs/edition.md#Издание)
    * [Основная информация](Docs/edition.md#Основная-информация)
    * [Добавление/удаление с книжной полки](Docs/edition.md#Добавление-или-удаление-с-книжной-полки)
5. [Премии](Docs/awards.md#Премии)
    * [Список премий](Docs/awards.md#Список-премий)
    * [Премия](Docs/awards.md#Премия)
    * [Конкурс](Docs/awards.md#Конкурс)
6. [Переводчик](Docs/translator.md#Переводчик)
    * [Основная информация](Docs/translator.md#Основная-информация)
    * [Список наград](Docs/translator.md#Список-наград-отдельно)
7. [Диктор](Docs/dictor.md#Диктор)
8. [Пользователь](Docs/user.md#Пользователь)
    * [Основная информация](Docs/user.md#Основная-информация)
    * [Список отзывов](Docs/responses.md#Отзывы-посетителя)
    * [Узнать id по login](Docs/user.md#Узнать-id-по-login)
8. [Отзывы](Docs/responses.md#Отзывы)
    * [Отзывы на все произведения автора](Docs/responses.md#Отзывы-на-все-произведения-автора)
    * [Отзывы на одно произведение](Docs/responses.md#Отзывы-на-одно-произведение)
    * [Отзывы посетителя](Docs/responses.md#Отзывы-посетителя)
    * [Новые отзывы на сайте](Docs/responses.md#Новые-отзывы-на-сайте)
10. [Авторизация](Docs/auth.md#Авторизация)
11. [Подписки](Docs/subscriptions.md#Подписки)
    * [Подписка на оповещения о новых произведениях/изданиях автора](Docs/subscriptions.md#Подписка-на-оповещения-о-новых-произведениях-или-изданиях-автора)
    * [Подписка на оповещения о новых изданиях с переводами переводчика](Docs/subscriptions.md#Подписка-на-оповещения-о-новых-изданиях-с-переводами-переводчика)
    * [Отмена подписки](Docs/subscriptions.md#Отмена-подписки)

**TODO**
* Издательства (`/publishers`, `/publisher/{id}`)
* Поиск по блогам (e.g. https://api.fantlab.ru/search-blog.json?q=David&blogs=0&t=t&alg=0&period=0&sortby=rel)
* Поиск по форуму (e.g. https://api.fantlab.ru/search-forum.json?q=David&t=t&forums=0&alg=0&period=0&sortby=rel)
* Краткий поиск (e.g. https://api.fantlab.ru/search.json?pretty=1&w=1,2,3&e=111,112&a=1,2)
* *OAuth*-авторизация
* Доописать *work* (выставление оценки и т.д.)
* Константы (использующиеся в качестве ключей в выдачах)

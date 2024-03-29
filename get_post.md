GET и POST

HTTP-методы GET и POST — самые распространённые способы отправить или получить данные с сервера. Но в разных случаях оба метода могут быть небезопасными или неудобными в использовании. В этой заметке рассмотрим, какой метод когда использовать.

**GET** — метод для чтения данных с сайта. Например, для доступа к указанной странице. Он говорит серверу, что клиент хочет прочитать указанный документ. На практике этот метод используется чаще всего, например, в интернет-магазинах на странице каталога. Фильтры, которые выбирает пользователь, передаются через метод GET.

:authority: htmlacademy.ru
:method: GET
:path: /tutorial/php/http-header

**POST** — метод для отправки данных на сайт. Чаще всего с помощью метода POST передаются формы.

URL-адрес запроса: https://htmlacademy.ru/consulting
Метод запроса: POST
Код состояния: 200

**Формат запроса**
Протокол HTTP очень прост и состоит, по сути, из двух частей — заголовков и тела запроса или ответа.

_Тело запроса_ — это информация, которую передал браузер при запросе страницы. Но тело запроса присутствует только если браузер запросил страницу методом POST. Например, если отправлена форма, то телом запроса будет содержание формы.

Сравнение заполненной формы и тела POST-запроса
Пример GET-запроса. Информация передаётся прямо в заголовке.

GET /blog/?name1=value1&name2=value2 HTTP/1.1
Host: htmlacademy.ru

Пример POST-запроса. Информация передаётся в теле запроса:

POST /blog/ HTTP/1.1
Host: htmlacademy.ru
name1=value1&name2=value2

**GET для безопасных действий, POST для опасных**

Говоря совсем просто, GET-запросы лучше не использовать с приватной информацией. Вот почему:

- _Они кэшируются_. Это значит, что логин и пароль, переданные через GET-запрос, могут остаться в интернете навсегда, например, в веб-архиве или кэше Гугла.
- _Остаются в истории браузера._ Чтобы узнать, какие данные отправлялись, достаточно нажать Ctrl+H.
- _Сохраняются в закладках и пересылаются._ Можно не обратить внимания и опубликовать в соцсетях или отправить ссылку с приватной информацией в GET-запросе.
- _Сохраняются в логах сервера._ Например, нельзя отправлять данные банковских карт через GET-запрос, так как это создаёт риски для пользователей.
Таким образом, любые важные данные — логины, пароли, данные карты, персональные данные — лучше передавать с помощью метода POST. Также метод POST поддерживает тип кодирования данных multipart/form-data, что позволяет передавать файлы.

_Ещё раз коротко:_
**GET**
Фильтры в интернет-магазинах
Передача параметров через ссылку
Другие безопасные запросы

**POST**
Любые формы с паролями или банковскими картами
Формы заявок с персональными данными
Отправка файлов
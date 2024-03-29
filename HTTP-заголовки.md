# Заголовки HTTP

**Заголовки HTTP** (англ. HTTP Headers) — это строки в HTTP-сообщении, содержащие разделённую двоеточием пару имя-значение. Формат заголовков соответствует общему формату заголовков текстовых сетевых сообщений ARPA. Заголовки должны отделяться от тела сообщения хотя бы одной пустой строкой.

Все заголовки разделяются на четыре основных группы:

**General Headers** (рус. Основные заголовки) — должны включаться в любое сообщение клиента и сервера.
**Request Headers** (рус. Заголовки запроса) — используются только в запросах клиента.
**Response Headers** (рус. Заголовки ответа) — только для ответов от сервера.
**Entity Headers** (рус. Заголовки сущности) — сопровождают каждую сущность сообщения.

Именно в таком порядке рекомендуется посылать заголовки получателю.

## Общий формат

- **Название** параметра должно состоять минимум из одного печатного символа (ASCII-коды от 33 до 126). Регистр символов в названиях не имеет значения. Заголовки с неизвестными именами должны игнорироваться. После названия сразу должен следовать символ двоеточия.
- **Значение** может содержать любые символы ASCII кроме перевода строки (код 10) и возврата каретки (код 13). Пробельные символы в начале и конце значения обрезаются. Последовательность нескольких пробельных символов внутри значения может восприниматься как один пробел. Регистр символов также не имеет значения (если иное не предусмотрено форматом поля).
  Предусматривается размещение значения на нескольких строках (перенос строки). Для указания переноса в начале следующей строки должен находиться хотя бы один пробельный символ.

Заголовки с одинаковыми названиями параметров, но разными значениями могут объединяться в один, только если значение поля представляет из себя разделённый запятыми список. Во всех остальных случаях значения более дальних заголовков должны перекрывать предыдущие. Поэтому прокси-сервера не должны менять порядок следования заголовков в сообщении. При этом порядок элементов списка обычно значения не имеет.

Пример с многострочными значениями и одинаковыми именами заголовков (обратите внимание на регистр символов и пробелы):

     content-type: text/html;          
                   charset=windows-1251
     Allow: GET, HEAD
     Content-Length: 356
     ALLOW: GET, OPTIONS
     Content-Length:   1984

Правильный компактный вариант преобразования и интерпретации:

     Content-Type: text/html;charset=windows-1251
     Allow: GET,HEAD,OPTIONS
     Content-Length: 1984

В этом случае недопустимо принимать значение Content-Length, равное 356. При объединении значений Allow, чтобы не потерять семантический смысл, была добавлена запятая в конец первого поля и убран бессмысленно дублирующийся элемент «GET».

## Применяемые в заголовках структуры

### Дата и время

Только дата указывается в заголовках `Date`, `Expires`, `Last-Modified`, `If-Modified-Since`, `If-Unmodified-Since`. Дата может присутствовать в заголовках `If-Range` и `Warning`.

В HTTP используется три формата:

- `Fri, 04 Jul 2008 08:42:36 GMT` — предпочитаемый формат по RFC 7231, подмножество формата по RFC 5322.
- `Friday, 04-Jul-08 08:42:36 GMT` — формат описанный в устаревшем RFC 850.
- `Fri Jul 4 08:42:36 2008` — результат функции asctime() языка ANSI C.
  RFC 7231 предписывает получателям данных быть готовыми обрабатывать отметки даты и времени во всех трёх форматах, а формировать отметки даты и времени только в предпочитаемом формате.

Время всегда указывается для часового пояса GMT (UTC+0). Год записывается четырьмя цифрами. День, час, минута и секунда дополняются нулями до двух символов. Для названий месяца и дня недели применяются трёхбуквенные стандартные сокращения на английском языке.

Дни недели начиная с понедельника: `Mon`, `Tue`, `Wed`, `Thu`, `Fri`, `Sat`, `Sun`.

Месяцы с января по декабрь: `Jan`, `Feb`, `Mar`, `Apr`, `May`, `Jun`, `Jul`, `Aug`, `Sep`, `Oct`, `Nov`, `Dec`.

### Байтовые диапазоны

При работе с фрагментами содержимого в специальных заголовках используются **байтовые диапазоны** (англ. byte ranges). В них можно указать как один фрагмент, так и несколько разделяя их запятыми «,». Диапазоны применяются в заголовках `Range` и `Content-Range`. В заголовке `Accept-Ranges` перечисляются только единицы измерения.

В байтовых диапазонах обязательно в начале указываются **название единиц измерения** за которым следует символ «=». В настоящий момент кроме единиц bytes никакие другие не применяются. За символом «=» располагаются сами диапазоны. Каждый из них является разделённой дефисом «-» парой натуральных чисел или нуля и натурального числа. Первый элемент указывает начальный байт, а второй — конечный. Нумерация в диапазонах начинается с нуля.

Начальный или конечный байт может быть не указан. При отсутствии последнего байта считается что речь идёт о фрагменте от начального байта до конца содержимого. Если отсутствует начало, то номер конечного байта воспринимается как количество запрашиваемых байт от конца содержимого.

Если первый байт больше чем последний, то диапазон считается синтаксически недействительным (англ. syntactically invalid). Поля заголовка, содержащие диапазоны с синтаксически недействительными значениями, игнорируются. Если первый байт выходит за пределы объёма ресурса, то диапазон игнорируется. Если последний байт выходит за пределы содержимого, то диапазон обрезается до конца.

Блок байтовых диапазонов считается выполнимым если в нём содержится хотя бы один доступный диапазон. Если же все диапазоны некорректны или выходят за пределы объёма ресурса, то серверу следует вернуть сообщение со статусом 416 (Requested range not satisfiable).

## Работа с заголовками

### Заголовки в HTML

Язык разметки HTML позволяет задавать необходимые значения заголовков HTTP внутри `<HEAD>` с помощью тега `<META>`. При этом название заголовка указывается в атрибуте `http-equiv`, а значение — в `content`. Почти всегда выставляется значение заголовка `Content-Type` с указанием кодировки, чтобы избежать проблем с отображением текста браузером. Также не лишним является указание значения заголовка `Content-Language`:

     <html>
     <head>
     <meta http-equiv="Content-Type" content="text/html;charset=windows-1251">
     <meta http-equiv="Content-Language" content="ru">
     ...

## Лингвистический календарь
В этом небольшом проекте собираем даты, которые можно назвать лингвистическими, в один большой языковедческий календарь, чтоб каждый день был повод штеко поднять бокал глокого вина.

В календарь можно включать любые события, которые связаны с языками, письменностями, словами, переводами, филологами и тому подобным. Например:
* Дни рождения учёных-лингвистов. Пока что таких дат больше всего: они были загружены автоматически с использованием базы знаний [Викиданные](https://www.wikidata.org/wiki/Wikidata:Main_Page).
* Официальные праздники: дни языков и письменностей. *[23 апреля](https://github.com/OloloPhilolo/calendar/blob/master/ru/04/23.json) в ООН отмечаются дни английского и испанского языков*.
* Открытие значимых языковых фестивалей, конференций, конкурсов, олимпиад. Если мероприятие периодическое, интересны дни его первого проведения. *[31 марта 2013 года](https://github.com/OloloPhilolo/calendar/blob/master/ru/03/31.json) состоялся I Минский Фестиваль языков*.
* Начало работы организаций, связанных с языками и лингвистикой. *[12 июня 2013 года](https://github.com/OloloPhilolo/calendar/blob/master/ru/06/12.json) заработала Академия языка гуарани*.
* Примечательные даты, связанные с функционированием языков в государстве (смена государственного языка, реформа орфографии, официальное признание языка диалектом или наоборот...). *[8 июня 2009 года](https://github.com/OloloPhilolo/calendar/blob/master/ru/06/08.json) Министерство образования и науки установило список нормативных словарей и справочников, зафиксировав в том числе равноправие мужского и среднего рода для слова «кофе»*.
* День публикации первой газеты / журнала / книги / фильма / сайта / анекдота / научного доклада на некотором языке. *[1 сентября 1889 года](https://github.com/OloloPhilolo/calendar/blob/master/ru/09/01.json) увидела свет первая газета на языке эсперанто: «La Esperantisto»*.
* Культурные окололингвистические события. *[1 сентября 2016 года](https://github.com/OloloPhilolo/calendar/blob/master/ru/09/01.json) состоялась премьера фильма «Прибытие»*, *[7 сентября 2003 года](https://github.com/OloloPhilolo/calendar/blob/master/ru/09/01.json) в белорусском Полоцке открыли памятник букве «Ў»*.
* Дни рождения слов. *[30 сентября 1836 года](https://github.com/OloloPhilolo/calendar/blob/master/ru/09/30.json), вероятно, было придумано слово «паровоз»*.
* Даты смерти языков — когда умирает последний носитель. *[10 апреля 1815 года](https://github.com/OloloPhilolo/calendar/blob/master/ru/04/10.json) из-за мощнейшего извержения вулкана исчез тамборский язык*.
* Нелингвистические события, повлиявшие на языки. *[4 октября 1957 года](https://github.com/OloloPhilolo/calendar/blob/master/ru/10/04.json) был запущен «Спутник-1», а его название вошло во многие языки мира*.

Поддержка событий, не имеющих закреплённой даты (например, день белорусской письменности проходит в первое воскресение сентября), пока не осуществляется.

## Формат
События одного дня хранятся как массив json-объектов в файле. Структура имени файла: *код языка/двузначный номер месяца/двузначный номер дня.json*, например *[ru/01/02.json](https://github.com/OloloPhilolo/calendar/blob/master/ru/01/02.json)* соответствует второму января. Пока что работа ведётся только над содержанием на русском языке, поэтому имеется лишь одна высокоуровневная папка *ru*.

Синтаксис json-файла следующий. Корневым объектом является массив событий. Массив записывается как заключённый в квадратные скобки список его элементов, разделённых запятой. Вот так:
```
[
  {
    // объект1
  },
  {
    // объект2
  },
  {
    // объект3
  }
]
``` 

Каждый json-объект — набор пар ключ-значение, где ключ — обязательно строка, а значение — произвольный объект. Пока что во всех файлах значения также являются строками. И ключ, и значение-строка берутся в кавычки и разделяются точкой с запятой, вот так: `"key1": "Значение ключа с именем key1"`. Сам json-объект представляется как заключённый в фигурные скобки список его пар ключ-значение, разделённых запятой. Вот так:

```
{
  "key1": "Значение ключа с именем key1",
  "name": "Значение ключа с именем name, вероятно имя той сущности, которую этот json-объект представляет",
  "ololo": "Ещё одно значение"
}
``` 

Пока что в файлах представлены следующие четыре ключа:
* **header** — заголовок события. Почти всегда представляет собой дату: например, «1 января» (для повторяющихся ежегодных событий, чаще всего праздников) или «1 января 2000» (для конкретных событий). 
* **text** — описание события. Хочется стремиться, чтобы описания были лаконичными, не более трёх-четырёх предложений, легко читались, но раскрывали основную суть события. Например, если это день рождения учёного, то стоит описать, чем он занимался. В тексте не стоит использовать кавычку `"`, поскольку она может сломать json-файл. Лучше обходиться «ёлочками» и 'одиночными кавычками'. Сейчас в файлах помимо текста встречаются также гиперссылки на записи паблика [«филолобайки дилетанта»](https://vk.com/ololo_philolo) Вконтакте. Они оформляются в соответствии с html-разметкой для гиперссылок: `<a href='адрес сайта'>текст ссылки</a>`. Пример можно посмотреть в день рождения паблика: *[ru/04/14.json](https://github.com/OloloPhilolo/calendar/blob/master/ru/04/14.json)*.
* **tag** — вспомогательный ключ, который связывает предмет события (родившегося учёного, отмечаемый праздник и т.д.) с элементом Викиданных. Например, [29 апреля 1935 года](https://github.com/OloloPhilolo/calendar/blob/master/ru/04/29.json) родился Андрей Зализняк, и это событие снабжено тегом *Q2371003*, потому что это идентификатор записи об Андрее Анатольевиче в Викиданных: https://www.wikidata.org/wiki/Q2371003. Данную связь предполагается использовать для автоматической обработки записей. Ключ проставлен у почти всех записей об учёных и у некоторых праздников.
* **type** — вспомогательный ключ, который характеризует событие. Пока что используются четыре типа событий: *birth* (день рождения), *death* (день ухода из жизни), *holiday* (ежегодный праздник), *event* (единоразовое событие).

Планируется поддержка также следующих полей:
* **source** — в лучших традициях Википедии ссылка на авторитетный источник информации.
* **attachments** — вложения, прежде всего изображения, связанные с событием: фотографии человека, образцы письменности, кадры с фестиваля, конференции или олимпиады и т.д. Если будет внедрено, то как сложный объект: массив вложений, где каждое вложение содержит собственно фотографию, описание и ссылку на источник.

Json-формат хорошо понятен компьютерам, так что проект можно использовать как источник информации для мобильного приложения или веб-сайта «Лингвистический календарь». Черновик такого сайта доступен на [Github Pages](https://ololophilolo.github.io/calendar/) (свёрстан на коленке за часок, не судите строго).

## Обратная связь
Вклад в Лингвистический календарь приветствуется: исправление уже имеющихся событий и внесение новых. Наполнять проект можно как с помощью Git / Github, так и контактируя с автором напрямую:
* через сообщения в паблике [«филолобайки дилетанта»](https://vk.com/ololo_philolo) Вконтакте;
* через бот [Телеграм-канала](https://t.me/ololo_philolo_bot) «филолобайки».

При внесении вклада можно отметить, указывать ли вас среди авторов, и если да, то каким образом. Актуальный список участников проекта доступен [здесь](https://github.com/OloloPhilolo/calendar/blob/master/Authors.txt).

## Лицензия
Содержимое файлов проекта предоставляется по свободной лицензии **[Creative Commons Attribution-ShareAlike 4.0 (CC BY-SA 4.0) Unported](https://creativecommons.org/licenses/by-sa/4.0/)**. Это значит, что материалы можно копировать, редактировать и использовать в коммерческих целях, но с указанием авторства и сохранением лицензии CC BY-SA 4.0. 
=================================
Библиотеки для Node.js приложений
=================================

Добро пожаловать в руководство по созданию веб-приложений на **Node.js**.
В рамках серии уроков мы будем делать веб приложение - записную книжку.
Приложение так и назовем - **Nodepad**. Название не особенно оригинальное,
зато легкое для понимания и четко формулирует цель.

Выбор фреймворков и инструментов
================================

Современные веб приложения базируются на нескольких компонентах:

- хранилище: реляционная БД, NoSQL
- библиотека для хранилища: простые инструкции, ORM
- веб сервер
- менеджер пакетов
- фреймворк для бэкенда
- фреймворк для фронтенда
- библиотеки для тестирования кода
- система контроля версий

Но окончательный выбор, в конце концов, зависит от ситуации. Мне приходилось
использовать те или иные технологии в зависимости от того, каким будет
процесс развертывания приложения. Когда я разрабатываю ПО с открытыми
исходными кодами, я предпочитаю использовать тот софт, который сможет легко
установить предполагаемый пользователь.

В рамках данного руководства выбора будет зависит от пожеланий читателей и
моего личного опыта.

Бэкенд
======

Создание веб приложений с помощью Node.js обычно предполагает использование
того или иного фреймворка. Если Вы почитаете наши еженедельные `сводки по Node.js`_,
то узнаете, что их уже достаточно много. Некоторые из них представляют из
себя попытки создания комплексных решений (набодобие Rails или Django),
другие же больше концентрируются на маршрутизации и HTTP-абстракциях.

В качестве примера популярного `Rails-подобного`_ фреймфорка можно привести
Geddy_, которому уже 7 месяцев (на момент написания поста: 01-11-2010) и он
активно развивается. Более простым примером является Sinatra_-подобный
фреймворк - Express_, который разрабатывается с июня 2009 года и все еще
регулярно обновляется.

.. _сводки по Node.js: http://dailyjs.com/tags.html#node
.. _Rails-подобного: http://rubyonrails.org/
.. _Geddy: http://github.com/mde/geddy
.. _Sinatra: http://www.sinatrarb.com/
.. _Express: http://github.com/visionmedia/express

Крупные фреймворки обычно предоставляют средства отображения ресурсов в
файлы в соотношении один-ко-многим через абстракцию модель-вид-контролер (MVC_).
Таким образом, проект проект может быть организован, например, так:

- Модели: user.js, note.js
- Контролеры: users.js, notes.js
- Представления: index.html (список элементов), edit.html, new.html

.. _MVC: http://ru.wikipedia.org/wiki/Model-View-Controller

Однако, далеко не все фреймворки используют шаблон MVC. Так в мире Node.js
много так называемых микро-фреймворков. Первоначально, я думал, что Express
так же относится к микро-фреймворкаам, но количество абстракций, которые он
предоставляет, говорит о том, что Express гораздо больше.

Я чувствую, что Express подходит как нельзя лучше для нашего проекта. Мы
могли бы использовать практически любой фреймворк, но Express сочетает в
себе много полезных вещей, которые сделают работу над проектов приятной,
при этом сам Express остается достаточно легковесным фреймворком.

Фронтэнд
========

Некоторые UI-фреймворки заметно сокращают количество рутинной работы при
разработке пользовательского интерфейса. За последнее время появилось
огромное количество JavaScript библиотек для разработки UI, среди
которых можно выделить следующие типы:

- Десктопо-подобные: Cappuccino, Sprout, Ext.js
- Низкоуровневые: jQuery, Prototype, MooTools
- Объединяющие низкоуровневые функции и богатый UI инструментарий: YUI
- Интерфейс-ориентированные, базирующиеся на низкоуровневых библиотеках: Scriptaculous, jQuery UI

Мне кажется, что Cappuccino и SproutCore будут слишком тяжелыми для
нашего проекта. А вот с помощью jQuery UI и `темы Aristo`_ можно
получить отличные результаты, при этом приложение не будет казаться
слишком тяжелым.

.. _темы Aristo: http://github.com/taitems/Aristo-jQuery-UI-Theme

Тестирование
============

В серии `Делаем фреймворк`_ я уже `упоминал`_ о том, что существует
`CommonJS спецификация по модульному тестированию`_. Nodeunit_ основан
на модуле assert из CommonJS, так что тесты будут не сильного отличаться
от тех, что Вы писали раньше.

.. _Делаем Фреймворк: http://dailyjs.com/tags.html#lmaf
.. _упоминал: http://dailyjs.com/2010/10/28/framework-part-36/
.. _CommonJS спецификация по модульному тестированию: http://wiki.commonjs.org/wiki/Unit_Testing/1.0
.. _Nodeunit: http://github.com/caolan/nodeunit

С другой стороны, Expresso_ предлагает *assert.response*, что делает
тестирование сервера чуть более простым. Expresso создан тем же автором,
что и Express (:ref:`TJ Holowaychuk <tj-holowaychuk>`), так что не
удивительно, что у этой библиотеки тестирования есть такая полезная
возможость.

.. _Expresso: http://visionmedia.github.com/expresso/

Пока я еще не определился, какую библиотеку использовать. Так что я
попробую обе, когда начну писать приложение, и выберу наиболее
подходящую из них.

Хранилище
=========

В последние два года в области хранилищ данных все посходили с ума.
Когда я начинал, были либо реляционные, либо объектные базы данных.
Последние у меня так и не получилось использовать. То есть, я в
основном пользовался Oracle, PostgreSQL или MySQL. Сейчас же
мейнстримом становится NoSQL, который предлагает такие инструменты
как CouchDB, MongoDB, Riak, Redis, Tokyo Cabine и многие другие.

Если Вы уже пользовались каким-либо из этих NoSQL фреймворков, то
знаете, что некоторые из них предоставляют JavaScript оболочки, которые
сильно облегчают жизнь. Кроме того, все NoSQL хранилища делят на:

- ключ-значение хранилища
- документо-ориентированное хранилища

Документ-ориентированное хранилище - звучит очень похоже на то, что
нам надо, учитывая что мы пишем блокнот.

Выбор системы хранения это одно, но тогда вам нужно выбрать библиотеку
для вашего языка и фреймворк - это совсем другое. Express не предоставляет
абстракции слоя модели, поэтому мы можем использовать любые системы хранилища
данных и их библиотеки.

Для этого проекта я бы хотел использовать MongoDB. Мне кажется что CouchDB
будет также хорошим выбором, но я написал много кода, использующего Mongoose_,
поэтому я хотел бы опираться на это знание.

.. _Mongoose: http://www.learnboost.com/mongoose/

API Mongoose делает код асинхронного обращения к БД менее громоздким.
Популярная "дефолтная" MongoDB библиотека для Node.js везде использует
функции обратного вызова (callback), а не чистые абстракции и цепочки
вызовов, что приводит к очень трудно читаемому коду.

До сих пор я использую Heroku_ и MongoHQ_, так как эти сервисы очень сильно
упростили мои сисадминские обязанности. В силу того, что технологии, лежащие
в основе, распространяются в исходных кодах, я могу скачать MongoDB и
запустить их локально для разработки, после чего уже разместить там, где
я плачу за поддержку.

.. _Heroku: http://heroku.com/
.. _MongoHQ: http://mongohq.com/

Ресурсы
=======

Я попытался написать эту часть руководства таким образом, чтобы показать,
как выбирать подходящие технологии для реальных открытых или комерческих
проектов. Если Вы находитесь в аналогичной ситуации, вот несколько полезных
ссылочек:

- `Сравнение JavaScript фреймворков`_
- `Модули для Node.js`_
- `NoSQL ресурсы`_
- `Список пакетов для NPM`_

.. _Сравнение JavaScript фреймворков:
   http://en.wikipedia.org/wiki/Comparison_of_JavaScript_frameworks
.. _Модули для Node.js: http://github.com/ry/node/wiki/modules
.. _NoSQL ресурсы: http://nosql-database.org/
.. _Список пакетов для NPM: http://npm.mape.me/

Далее
=====

В следующей части, я пройдусь по окружению для разработки и созданию базового
приложения.

В целом, руководство будет покрывать следующие области:

- установка всего, что необходимо
- создание простого Express приложения
- создание тестов для Node.js приложений
- создание насыщенного интерфейса пользователя с jQuery UI
- использование Mongoose с Node.js
- развертывание исходного кода

Как и в серии `Делаем фреймворк`_, некоторые области могут занять несколько
недель (частей), чтобы полностью покрыть соответствующую тему.

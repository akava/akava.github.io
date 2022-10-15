---
layout: post
permalink: /blog/39-:slug/
title:  "Что такое Lean epic? Или как поженить ужа с ежом."
date:   2022-10-15 14:14:06 +04:00
featured: False
tags: 
- name: product management
  slug: product_management
- name: lean
  slug: lean
- name: agile
  slug: agile
---

Долго не мог совместить Lean/Kanban и современную организацию работ с разбиением на Features и на Epics, которые используются в большинстве agile-процессов. Причем если с фичами все понятно: бьем типичную фичу на части, начиная с наименьшей части (MVP) и развиваем ее итерациями, где каждая итерация – это новая фича. 

Т.е. как совмещать lean и features созрело давно, но было непонятно как встроить это в Product Management и планирование крупных кусков работ. Эпики долго не давались. И вот недавно, как мне кажется, у меня получилось.

### Что такое Эпик.
Можно выделить 2 подхода к определению того, что такое Эпик:
* Эпик – законченный кусок функциональности, который приносит пользу end-2-end.
* Эпик – это какая-то инициатива, направление, которое нам помогает сфокусироваться на достижении этой цели. 

Первый вариант – это то, что используется чаще всего в индустрии. У Эпика есть четкое описание, его scope, так и видишь результат, читая его. Да, его не просто добиться (это будет серия фич, которые разработчики будут бить на Story и работать над ними). Хочется сразу же применить к Epic подход выше, выделить MVP Epic и развивать его дальше, но этот подход порочен: эпики – максимальный уровень группировки работы, с которой работает команда. Их не должно быть много, иначе у нас будет огромный бэклог и мы будем тратить много времени на их поддержку.

Ок. Эпик – это законченный кусок функциональности, который не стоит бить на части, выделяя MVP и итерации. Тогда, получается, мы заранее знаем что мы хотим получить и можем расписать фичи на весь объем работ. Где тут гибкость? Где циклы обратной связи, где обучение и реакция на поведение пользователей? Старый добрый waterfall.  <!--more-->

### Эпик, как инициатива, идея и направление.
Второй вариант. Эпик – это инициатива, идея, направление, которое нам помогает сфокусироваться на достижении этой цели.  Достаточно абстрактно, но ок. Допустим мы сформулировали идею, знаем как мерять движение в сторону цели (через метрики, KR из OKR, например). 

Что это нам дает? Например то, что сюда очень хорошо ложатся Feature MVP и итерации. Мы можем накидать туда идеи фич, выделить в каждой идеи ее минимальную реализацию, сделать ее понятной команде. И реализовать. Померять результат (движемся к цели или нет), если он удовлетворителен – развиваем фичу дальше итеративно. Нет – выкидываем функционал и пробуем другие идеи. Настоящий agile.

### Какие выводы можно сделать.
* Нам не нужно прорабатывать Эпик досконально, можно начать с пары идей. А значит избежать analysis paralysis и начать эксперименты раньше.
* *Нам не нужно бояться, что мы что-то упустили при планировании эпика. Мы всегда можем добавить новых фич позже, когда у нас будет больше информации. Привлечь команду к обсуждению новых идей, ...
* Мы можем ранжировать эпики. Меняя приоритеты. Допустим мы выполнили 60% фич, которые лежат в эпике (а мы ведь помним, что мы можем добавлять новые). Эпик не закончен, мы знаем, что там есть куда двигаться, что делать, чтобы стало лучше (мы даже померять это "лучше" можем). Но есть более важная работа и мы хотели бы ее сделать. Ничего страшного – понижаем приоритет эпика, замораживаем работы над ним (мы уже достаточно многого добились) и занимаемся другими вещами. 
 * Через время мы можем вернуться к этому Эпику и продолжить над ним работу. Или не продолжить. Закрыв Эпик с чистой совестью – мы ведь уже достигли хорошего результата.
* Работу над такими Эпиками так же можно планировать. Брать их из бэклога в "спринт" (длинной в квартал, например). Хоть в Lean/Kanban и нету спринтов, но можно договориться фиксировать приоритеты эпиков на какой-то период, чтобы нас не бросало из стороны в сторону каждый спринт.

### Ложка дегтя.
Такие Эпики невозможно оценивать. Они "бесконечные", непонятные. Да, их можно ограничивать (time-box, скажем не больше 1/3 капасити команды на итерацию), но не оценить. Ни посчитать, и ни сказать что же мы получим в конце, скажем, года мы не можем. Мы даже не сможем сказать что же получиться в конце. Проектных менеджеров будет сильно колбасить :)

Меня греет только то, что текущие способы оценки – все равно фикция. 

Вот что нам дает понимание, что к концу года мы сможем закончить "рабочее место администратора", "автоматизированную обработку запроса пользователя", ..? Мы станем зарабатывать больше денег, у нас будет меньше %% ошибок и возвратов, вы привлечем больше пользователей, они будут более довольны? Нет. Мы просто, по сути, говорим, что к концу года что-то сделаем, а как это повлияет на результат – это не к нам. Не говоря уже о том, что отказаться от таких эпиков очень сложно. Мы ведь уже пообещали...
 
Подход с эпиками-направлениями, которые мы умеем мерять, этого недостатка лишен – мы изначально заявляем измеримые цели. Да, мы не знаем что у нас будет в конце года, но знаем, что мы сфокусируемся на вещах, важных для бизнеса и принесем пользу. И, главное, можем гибко (agile) менять приоритеты и экспериментировать.
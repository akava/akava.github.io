---
layout: post
permalink: /blog/50-:slug/
title:  "7 стадий стартапа. Взгляд архитектора"
date:   2024-06-02 19:11:13 +03:00
#featured: True
unlisted: True
tags: 
- name: Стартап
  slug: startup
- name: Архитектура
  slug: archtiecture
---

Грамотная [статья](https://www.latitud.com/blog/stages-of-a-startup), классифицирующая стадии жизненного цикла компании. Начиная с идеи (основание стартапа) до поиска Product-Market-Fit (через MVP и поиск инвестора для экспериментов), далее идет выход на рынок и рост (growth/scale), после чего идет этап оптимизации (Maturity). 

Сразу же захотелось наложить эту классификацию на модель из [Digital Practitioner](https://www.opengroup.org/dpbok) уж очень стадии близки и ровно ложатся друг на друга: Team of teams – однозначно стадия роста, Enterprise –  стадия оптимизации.

А еще наложить на модель из книги [Crossing the Chasm](https://en.wikipedia.org/wiki/Crossing_the_Chasm#/media/File:Technology-Adoption-Lifecycle.png). Product-Market-Fit – как раз этап преодоления пропасти.

# Этапы жизненного цикла
(ниже каждого пункта идет чеклист успешного его прохождения)

1. Ideation
	* You've found a community with a problem that has no satisfactory solution;
	* You've validated that enough people would pay to get this problem solved (market potential);
	* You've formulated a hypothesis of solution to this problem.
2. MVP
	* You've built a minimum viable product, with the most basic version of the key feature you're offering;
	* You've tested your MVP's value and channel proposition, gathering feedbacks from potential customers and learning from them;
	* You've decided whether to refine your minimum viable product or to pivot to a new MVP.
3. Investment
	* You've prepared your startup to receive investments the right way;
	* You've checked what round you should be aiming for at this moment;
	* You've studied the best investors for your business, prepared your pitch, and started to foster 
4. Product-market fit
	* You're in a good market with a product that satisfies this market;
	* You're seeing consistent and predictable user and revenue growth;
	* You're seeing good customer retention metrics.
5. Go-to-market
	* You've found marketing, sales, pricing, and customer retention strategies that keep your CAC and LTV healthy;
	* These strategies are not easily copied by the the competition, as you've built moats around them;
	* You have a repeatable, scalable, and profitable revenue generation model.
6. Growth
	* You've nailed product-market fit, go-to-market, and profitability;
	* You've seen sustainable growth for a good period of time;
	* You've seen successful strategies to keep that growth rate going, such as making acquisitions or entering new markets.
7. Maturity
	* Вы красавчик. Радуйтесь жизни 
	* Оптимизируйте продукт или же:
		* переходите к пункту 4 (с другим продуктом);
		* или п5 (с другим маркетом);
		* или п1 (с другой идеей).

# Применение к архитектуре и архитекторам

## Growth
Мне лучше всего подходят компании роста (growth/scale). Я там чувствую себя лучше всего – продукт понятен, рынок его принимает, соответственно есть деньги. Начинается экспансия. Экспансия всегда сопровождается с ростом персонала, а люди, когда их больше 10 начинают мешать друг другу (а когда их 50+ то тем более). Поэтому начинает играть первую скрипку организационная архитектура, выделение платформенного слоя и независимое масштабирование разных этапов Value Stream.

[Team Topologies](https://teamtopologies.com/) начинает играть важную скрипку. Stream aligned teams появляются из Value Stream. 

## Maturity
ЕПАМ, в основном, работает с компаниями этапа Maturity/Optimization. Тут нужны большие платформы, серьезный гаверненс (т.е. разные борды для наведения порядка), жесткая рука "счетовода", ...

Я не люблю работать в таких компаниях (умею и ничего против не имею, но не люблю) – у меня, как инженера, всегда ощущение, что "пациент" уж слишком запустил себя. Причем большинство проблем он создал себе сам и их можно было избежать просто (что совсем не просто) следуя индустриальным лучшим практикам (best practices) 2-3 года назад. Да, тупо, следовал бы лучшим практикам. Причем не обязательно брать что-то образца 24го или даже 14 года. Возьмите Digital Practitioner – посмотрите что вам нужно на этапе Team of Teams и при переходе к этапу Enterprise и возьмите оттуда ТОЛЬКО здравый смысл.

## Go-to-Market
На этом этапе происходит усложнение продукта, увеличение количества фич. Выделение "commodity" сервисов в платформу.

Вклад в user experience. Для архитектора это, в основном, в надежность и доступность.

## Product-Market-Fit
На данном этапе важна гибкость и умение быстро ставить эксперименты. Т.е. архитектура должна поддерживать эксперименты. И, главное, не ограничивать – иначе ее "выкинут". Необходимо уметь считать метрики – чтобы понять успешность экспериментов.

С точки зрения разработки происходит развитие dev-excellence процессов (если об этом не позаботились на предыдущих этапах).

## Ideation – Investment
Умение быстро "на коленке" слепить прототип, потом MVP, уметь показывать домонстрации как пользователям так и инвесторам.

Архитектор не нужен – достаточно адекватного Тим Лида в роли CTO. Не мешать разработчикам "творить" и умение собрать демо-стенд для "звонка инвесторам через пол часа" – ключевые требования.

# Каждому этапу свой архитектор

Важно понимать какой этап жизненного цикла компании соответствует вам, как разработчику/архитектору. Успешность на одном из этапов абсолютно не означает успешность не только на следующих, но и на предыдущих. Обращайте на это внимание.

Какой вы архитектор? Расскажите об этом в обсуждении: (ссылка на коментарии).

---
layout: post
permalink: /blog/31-:slug/
title:  "Обзор конференции Microsoft //build/"
date:   2015-06-01 02:14:05 +03:00
featured: False
tags: 
- name: windows
  slug: windows
- name: dotnet
  slug: dotnet
- name: microsoft
  slug: microsoft
---
Возможно вы знаете про конференцию [MS //build/](http://www.buildwindows.com/) прошедшую в конце апреля в Сан Франциско. Это самое большое событие Майкрософт в году на котором она анонсирует новые продукты, а так же задает направление развития на весь год.

<iframe src="https://onedrive.live.com/embed?cid=CEB20B23FFD270C6&resid=ceb20b23ffd270c6%21361&authkey=AGYEdZQzq2aK3hc&em=2" width="700" height="570" frameborder="0" scrolling="no"></iframe>

Моя версия краткого содержания //build/ ниже. Если у вас нет времени читать, то можете <!--more--> [просмотреть презентацию](https://onedrive.live.com/view.aspx?cid=CEB20B23FFD270C6&resid=ceb20b23ffd270c6!361&app=PowerPoint), которую я с Алексеем Горшколепом готовил для одного из наших Техтоков.

В этом году прозвучало 220 докладов на разнообразные тематики: от выхода Windows 10, Visual Studio 2015, .Net Core 5, Universall Applicaitons, запуску Android и iPhone приложений под Windows,...  и  до ответа [микросервисам](http://martinfowler.com/articles/microservices.html) в виде [Azure Service Fabric](http://channel9.msdn.com/Events/Build/2015/2-640), [анализа Больших Данных с помощью HDInsight](http://channel9.msdn.com/Events/Build/2015/2-690) и [визуализации их (данных) на Bing Maps ](https://channel9.msdn.com/Events/Build/2015/2-645). Майкрософт будет продолжать развивать облачную платформу Azure. Представила Office 365 как общую платформу, а не набор отдельных приложений. Windows 10, как единую платформу для устройств от Raspberry Pi до HoloLens и Surface Hub.

Все просмотреть абсолютно нереально, но названия, слайды и интересующие меня презентации я просмотрел. Благо все выложено в интернет и даже есть [скрипт, который позволяет закачать весь //build/ на компьютер](https://gallery.technet.microsoft.com/All-Videos-and-Slides-from-64a86489) (1,5Gb слайдов и 250Gb видео).

Поехали.

### Windows 10 и Universal Apps

![](https://dl.dropboxusercontent.com/u/15949847/Blog/MS%20Build%2015/Win10.PNG)

Windows 10 будет единой платформой для всех устройств вне зависимости от их размеров и возможностей. Это возможно с помощью Universal Applications, которые будут работать на любых устройствах и экранах (магии нет: разработчику придется постараться для этого. Майкрософт предлагает что-то похожее на принципы [Responsive Web Design](http://en.wikipedia.org/wiki/Responsive_web_design), но для нативных приложений).

В Windows Store наконец попадут десктопные приложения, а так же Web-приложения (да, свой сайт можно завернуть в контейнер и он будет работать без браузера), Android/iOS приложения. Ну и музыка с видео там тоже будет.

Целый доклад посвящен тому как сделать универсальные приложения универсальными: [Design: UX Patterns and Responsive Techniques for Universal Windows Apps](http://channel9.msdn.com/Events/Build/2015/2-658).

Появиться возможность связывать нативные приложения вместе [App-to-App Communication: Building a Web of Apps](http://channel9.msdn.com/Events/Build/2015/3-765).

И многое другое.

UDP. Как раз сегодня [Microsoft анонсировала выход Windows 10](http://blogs.windows.com/bloggingwindows/2015/06/01/hello-world-windows-10-available-on-july-29/): она будет доступна 29 Июля.

### .Net 2015

![](https://dl.dropboxusercontent.com/u/15949847/Blog/MS%20Build%2015/dot_net_platform.PNG)

Будет 2 версии фреймворка: .Net Framework 4.6 (это то что уже есть сейчас) и .Net Core 5 -- кросс платформенная версия рантайма плюс основных библиотек на которой будет работать ASP.Net 5 и Универсальные Приложения.

Основная презентация: [A Lap Around .NET 2015](http://channel9.msdn.com/Events/Build/2015/2-614).

Анонсирован выход Roslyn компилятора (платформы) вместе с Visual Studio 2015. Он пока еще Release Candidate, но разработчики уверяют, что на него уже можно переводить продакшен проекты, а RC это всего лишь маркетинговый ход. [.NET Compiler Platform (Roslyn)Analyzers and the Rise of Code-Aware Libraries](http://channel9.msdn.com/Events/Build/2015/3-725)

В студию включат (урезанную) версию [Xamarin](http://xamarin.com/), а так же [Apache Cordova](https://cordova.apache.org/g).

Очень, очень сильно переделали ASP .Net 5. Запуск на CoreCLR (т.е. под Linux и Mac). Возможность "носить" с собой рантайм (не нужно просить админов поставить специальную версию .net). Проектный файл теперь json, конфиг файл заменили на ini формат. С помощью Roslyn разогнали компиляцию, которая теперь происходит в фоновом режиме. Подробнее: [Introducing ASP.NET 5](http://channel9.msdn.com/Events/Build/2015/2-687) и [Deep Dive into ASP.NET 5](http://channel9.msdn.com/Events/Build/2015/2-726)

### Visual Studio 2015

Будет всего 3 версии Студии: Community Edition, Professional и Enterprize. Многие фичи перекочевали из Enterprize в Professional, например Code Lense.

В студии появится свой Memory Profiler (Performance profiler уже был, но он тоже улучшится).

### Архитектура

Меня больше интересуют архитектурные вопросы: как Майкрософт предлагает создавать сложные системы, с помощью каких кубиков. По докладам этой тематики хорошо видно, что MS делает ставку на облака и Azure. Все архитектурные доклады связаны с Azure.

[Surviving Success: Architecting Web Sites and Services for Rapid Growth](http://channel9.msdn.com/Events/Build/2015/2-642) рассказывает почему важно иметь хорошую архитектуру и почему Azure с функцией автоскейлинга это хороший выбор. 


[Azure’s Next Generation Compute Platform ](http://channel9.msdn.com/Events/Build/2015/3-618) -- обзор новых возможностей Azure от Марка Русиновича. На котором представляется, в частности, Azure Service Fabric. Очень рекомендую.

Доклад про саму Service Fabric [Microsoft Azure Service Fabric Architecture](http://channel9.msdn.com/Events/Build/2015/2-640) и как строить на нем приложения [Building Resilient, Scalable Services with Microsoft Azure Service Fabric](http://channel9.msdn.com/Events/Build/2015/2-700). Выглядит все очень здорово. Обязательно нужно попробовать.

Кто еще не знает про Docker, вам сюда:  [Thinking in Containers: Using Docker to //build/ on Azure](http://channel9.msdn.com/Events/Build/2015/2-683). Ну и доклад про докер был бы неполон без новых нано-серверов от MS: [Nano Server: A Cloud Optimized Windows Server for Developers](http://channel9.msdn.com/Events/Build/2015/2-755)

Майкрософт выводит в продакшен Application Insights -- платформа по сбору метрик и статистики работающих приложений. Из коробки есть поддержка .net, Ruby, Java, Android, Python, iOS, PHP, node JS. Есть достаточно приличная бесплатная версия.

Статистику по посещениям, ошибкам, загрузки процессора и памяти вы получите автоматически, но основное назначение платформы это анализ поведения пользователей, что уже требует ручной настройки. Но Майкрософту тоже есть что предложить: [Application Insights for Any App: A Must-Have Tool for Understanding Your Customers](http://channel9.msdn.com/Events/Build/2015/3-624).

![](https://dl.dropboxusercontent.com/u/15949847/Blog/MS%20Build%2015/DataFactory.PNG)

Много внимания уделено Big Data и Big Data Analysis. Майкрософт активно развивается в этом направлении: [Building Data Analytics Pipelines using Azure Data Factory, HDInsight, Azure ML and more](http://channel9.msdn.com/Events/Build/2015/2-690), [Gaining Real-Time IoT Insights Using Azure Stream Analytics, Azure ML, and Power BI ](http://channel9.msdn.com/Events/Build/2015/2-708), [Visualizing Business Data on any Device with Bing Maps](http://channel9.msdn.com/Events/Build/2015/2-645).

Если кто интересуется анализом данных, но не слышал про [Power BI](https://powerbi.microsoft.com/) -- рекомендую ознакомиться.
![](https://dl.dropboxusercontent.com/u/15949847/Blog/MS%20Build%2015/PowerBI.PNG)


### Ссылки на доклады пачками

Ниже ссылки на понравившиеся мне доклады по .Net и архитектуре. Пользуйтесь на здоровье.

#### .Net

- [A Lap Around .NET 2015](http://channel9.msdn.com/Events/Build/2015/2-614)
- [What's New in C# 6 and Visual Basic 14](http://channel9.msdn.com/Events/Build/2015/3-711)
- [Introducing ASP.NET 5](http://channel9.msdn.com/Events/Build/2015/2-687)
- [Deep Dive into ASP.NET 5](http://channel9.msdn.com/Events/Build/2015/2-726)
- [Entity Framework 7 Data for Web, Phone, Store, and Desktop](http://channel9.msdn.com/Events/Build/2015/2-693)
- [.NET Compiler Platform (Roslyn)Analyzers and the Rise of Code-Aware Libraries](http://channel9.msdn.com/Events/Build/2015/3-725)
- [Historical Debugging with IntelliTrace in Visual Studio 2015](http://channel9.msdn.com/Events/Build/2015/3-771)
- [Diagnosing Issues with Cloud Applications Hosted in Azure IaaS and PaaS Using Visual Studio](http://channel9.msdn.com/Events/Build/2015/4-754)
- [Introducing the Windows 10 App Model](http://channel9.msdn.com/Events/Build/2015/2-617)
- [Modern Web Tooling in Visual Studio 2015](http://channel9.msdn.com/Events/Build/2015/2-675)
- [Debugger Tips and Tricks for .NET Developers with Visual Studio 2015](http://channel9.msdn.com/Events/Build/2015/3-677)


#### Архитектура

- [App LifecycleFrom Activation and Suspension to Background Execution and Multitasking in Un](http://channel9.msdn.com/Events/Build/2015/3-626)
- [Cross-Platform Continuous Delivery with Release Management to Embrace DevOps](http://channel9.msdn.com/Events/Build/2015/3-649)
- [Azure App Service Architecture](http://channel9.msdn.com/Events/Build/2015/2-628)
- [Microsoft Azure Service Fabric Architecture](http://channel9.msdn.com/Events/Build/2015/2-640)
- [Surviving SuccessArchitecting Web Sites and Services for Rapid Growth](http://channel9.msdn.com/Events/Build/2015/2-642)
- [Building Highly Scalable and Available SaaS Applications with Azure SQL Database](http://channel9.msdn.com/Events/Build/2015/2-678)
- [Thinking in ContainersBuilding a Scalable, Next-Gen Application with Docker on Azure](http://channel9.msdn.com/Events/Build/2015/2-683)
- [Building Data Analytics Pipelines Using Azure Data Factory, HDInsight, Azure ML and More](http://channel9.msdn.com/Events/Build/2015/2-690)
- [Building Resilient, Scalable Services with Microsoft Azure Service Fabric](http://channel9.msdn.com/Events/Build/2015/2-700)
- [Windows ContainersWhat, Why and How](http://channel9.msdn.com/Events/Build/2015/2-704)
- [Gaining Real-Time IoT Insights using Azure Stream Analytics, AzureML and PowerBI](http://channel9.msdn.com/Events/Build/2015/2-708)
- [Nano ServerA Cloud Optimized Windows Server for Developers](http://channel9.msdn.com/Events/Build/2015/2-755)
- [When Bad Things Happen to Good AppsTroubleshooting Applications on Azure App Service](http://channel9.msdn.com/Events/Build/2015/2-764)
- [The Next Generation of Azure Compute Platform with Mark Russinovich](http://channel9.msdn.com/Events/Build/2015/3-618)
- [Application Insights for Any AppA Must-Have Tool for Understanding Your Customers](http://channel9.msdn.com/Events/Build/2015/3-624)
- [On the Shoulders of GiantsBuilding Apps that Consume Modern SaaS Endpoints with Visual Stu](http://channel9.msdn.com/Events/Build/2015/3-759)
- [App-to-App CommunicationBuilding a Web of Apps](http://channel9.msdn.com/Events/Build/2015/3-765)

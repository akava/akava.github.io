---
layout: post
title:  "Как настроить Network Tracing в .net"
date:   2014-02-25 03:31:13 +03:00
featured: False
---
Если вы, как и я, изучали .net в "боевых условиях" под лозунги "вперед на мины, за вами Родная Компания", а первым встретившимся вам инструментом логирования был log4net, вы, позже, узнали про стандартные средства логирования в .net (`System.Diagnostics.Trace`, например), но не видели смысла разбираться с еще одним логером, когда вас старый полностью устраивает. 
То, вполне вероятно, что вы тоже не знали, что у стандартного логера есть особенность, о которой желательно знать всем. 

Особенность эта в том, что код .net фреймворка уже прошит его вызовами. И что для получения всей этой (иногда жизненно важной) информации вам всего лишь нужно добавить несколько строчек в конфиг.
И пусть вы и дальше будете продолжать пользоваться log4net, знание, что вы всегда можете включить дополнительное логирование, не раз может вам пригодиться. Мне это уже пригодилось. Но обо всем по порядку.

#### История (почти) детективная о неработающем приложении)))

Разрабатывали мы клиента, который скачивал данные из одного облачного хранилища. Разработали, оттестировали на рабочей машине, на тестовом сервере, выкатили на продакшен и... ничего. Программа данные не качает, молчит, а через некоторое время валится с ошибкой.

На сервере ничего установить нельзя, ни дебагер, ни трассировщик, ничего стороннего. Ну с таким мы уже сталкивались. Прошили клиента лог-сообщениями; запустили, собрали лог; уточнили место, в котором валится, прошили плотнее; обнаружили место ошибки. Ура! Нет, не ура. Этой строчкой оказался вызов библиотеки провайдера данных. Этот вызов, в свою очередь, отправлял HTTP REST запрос и получал ответ от сервера. Логика вроде не сложная, но в ответ от сервера нам приходила пустота (т.е. `null`). На рабочих машинах все в порядке. На таком же тестовом сервере, с тем же [теоретически] набором ПО и настройками  работает. А на продакшен сервере не работает.

Нам бы поставить [fiddler](http://www.telerik.com/fiddler) и посмотреть, что же происходит "под капотом", но нельзя. Сервак-с. Появились безумные мысли дизассемблировать библиотеку провайдера и напихать туда логирования (благо .net). Но, к счастью, мы наткнулись на сообщение о том, что можно включить логирование в самом .net Framework-е через конфиг файл.

Мы его включили, запустили приложение, забрали логи, проанализировали, стукнули себя по лбу, исправили. Все заработало. (В чем была ошибка, я говорить не буду. Стыдно.)

#### Как все же настроить Network Tracing

Само сообщение: [How to: Configure Network Tracing](http://msdn.microsoft.com/en-us/library/ty48b824.aspx). В нем содержится конфиг файл, который включает логирование в нэймспэйсе System.Net. Добавили эти строчки в конфиг и обнаружили, что в лог пишется слишком много ненужной нам информации. Поменяли параметр `tracemode="includehex"` на `tracemode="protocolonly"` (16-ричные коды нам точно не нужны), убрали логирование в `System.Net.Sockets` и `System.Net.WebSockets`.

Вот итоговый конфиг файл:

    <system.diagnostics>
      <sources>
        <source name="System.Net" tracemode="protocolonly" maxdatasize="1024">
          <listeners>
            <add name="System.Net"/>
          </listeners>
        </source>
        <source name="System.Net.Cache">
          <listeners>
            <add name="System.Net"/>
          </listeners>
        </source>
        <source name="System.Net.Http">
          <listeners>
            <add name="System.Net "/>
          </listeners>
        </source>
      </sources>
      <switches>
        <add name="System.Net" value="Verbose"/>
        <add name="System.Net.Cache" value="Verbose"/>
        <add name="System.Net.Http" value="Verbose"/>
      </switches>
      <sharedListeners>
        <add name="System.Net"
          type="System.Diagnostics.TextWriterTraceListener"
          initializeData="network.log"
        />
      </sharedListeners>
      <trace autoflush="true"/>
    </system.diagnostics>

Пример лог вывода:

    System.Net Verbose: 0 : [4456] WebRequest::Create(#####################URL########################)
    System.Net Verbose: 0 : [4456] HttpWebRequest#58870012::HttpWebRequest(#####################URL########################)
    System.Net Warning: 0 : [4456] The Registry value 'Software\Microsoft\Windows NT\CurrentVersion\InstallationType' was either empty or not a string type.
    System.Net Information: 0 : [4456] Current OS installation type is 'Unknown'.
    System.Net Information: 0 : [4456] RAS supported: True
    System.Net Verbose: 0 : [4456] Exiting HttpWebRequest#58870012::HttpWebRequest() 
    System.Net Verbose: 0 : [4456] Exiting WebRequest::Create() 	-> HttpWebRequest#58870012
    System.Net Verbose: 0 : [4456] HttpWebRequest#58870012::GetRequestStream()
    System.Net Information: 0 : [4456] Associating HttpWebRequest#58870012 with ServicePoint#3741682
    System.Net Information: 0 : [4456] Associating Connection#33675143 with HttpWebRequest#58870012

    System.Net Information: 0 : [4456] ConnectStream#20234383 - Sending headers
    {
    Authorization: Basic *************************************************==
    Accept: application/json, application/xml, text/json, text/x-json, text/javascript, text/xml
    User-Agent: RestSharp 102.7.0.0
    Content-Type: application/json
    Host: ************
    Content-Length: 2430
    Accept-Encoding: gzip, deflate
    Connection: Keep-Alive
    }.
    System.Net Verbose: 0 : [4456] Exiting HttpWebRequest#58870012::GetRequestStream() 	-> ConnectStream#20234383
    System.Net Verbose: 0 : [4456] ConnectStream#20234383::Write()

    System.Net Verbose: 0 : [4456] Data from ConnectStream#20234383::Write
    System.Net Verbose: 0 : [4456] (printing 1024 out of 2430)
    System.Net Verbose: 0 : [4456] <<{"createdBy":null,"createdAt":null,"fields":{"ContactIDExt":"\{\{Contact.Field(C XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX>>
    System.Net Verbose: 0 : [4456] Exiting ConnectStream#20234383::Write() 
    System.Net Verbose: 0 : [4456] ConnectStream#20234383::Close()
    System.Net Verbose: 0 : [4456] Exiting ConnectStream#20234383::Close() 
    System.Net Verbose: 0 : [4456] HttpWebRequest#58870012::GetResponse()

#### Нужно поднимать основы

Несмотря на то, что я уже больше 8 лет работаю с платформой .net, о многих вещах я до сих пор не знаю. О базовых, можно сказать, вещах. Патерны, архитектура, Эджайлы, Канбаны, REST, HighLoad, DI, IoC, SOLID, ... На это время у меня находится. А вот взять и разобраться с тем, что уже предоставляют мне мои инструменты..., на это у меня времени нет :(

Нужно будет обязательно разобраться со стандартным логированием, посмотреть, какие еще стандартные библиотеки предоставляют такой сервис (предположительно все библиотеки прикладного уровня). А так же раздобыть книжку с обзором средств диагностики в .net фреймворке. Может, вы такую посоветуете? И, наконец, дочитать [Рихтера CLR via C#](http://www.ozon.ru/context/detail/id/7425674/).

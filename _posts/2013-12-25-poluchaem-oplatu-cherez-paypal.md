---
layout: post
permalink: /blog/23-:slug/
title:  "Получаем оплату через PayPal"
date:   2013-12-25 02:19:27 +03:00
featured: False
tags: 
- name: paypal
  slug: paypal
---
Закончил интеграцию нашей площадки с платежной системой [PayPal](http://paypal.com/). В моем случае, была небольшая особенность -- мы уже принимаем платежи с [Робокассы](http://robokassa.ru/) и нам хотелось бы получить похожий воркфлоу при оплате. Разных вариантов интеграции у PayPal очень много и самой большой "сложностью" был поиск нужного варианта, совпадающего с уже существующим воркфлоу.

Воркфлоу наш очень прост: 
<!--more-->

- пользователь вводит сумму, нажимает кнопку, переходит на сайт платежной системы
- оплачивает и возвращается системой к нам
- мы дальше проверяем статус оплаты и делаем необходимые нам манипуляции. 

В итоге у меня все получилось, хотя и не без маленьких косяков (как же без них).

#### Что нам понадобится

- [PayPal REST API SDK](https://paypal.github.io/#payments) Я писал на .net, но SDK есть для многих платформ, а даже если нет, то это ведь REST и OAuth -- можно подключиться и без SDK.

- [Инструкция по взаимодействию с API](https://developer.paypal.com/webapps/developer/docs/integration/web/accept-paypal-payment/)

- [Интерактивный гайд с примерами кода](https://devtools-paypal.com/guide/pay_paypal/dotnet?interactive=ON&env=sandbox) Код я брал прямо оттуда, причесывал, правил баги, заполнял "пустоты" (те самые косяки выше).

#### Шаг 1: Настройка PayPal

Заходим на [developer.paypal.com](https://developer.paypal.com). Для этого подойдет обычный аккаунт paypal. Переходим к вкладке [Applications](https://developer.paypal.com/webapps/developer/applications/myapps).

Создаем новое приложение. Сложностей у вас не должно возникнуть. Из важных параметров: "Application return URL". Это адрес на который PayPal будет направлять пользователя после оплаты (или отмены). Так же обратите внимание на Client ID и Secret. Это ключи, по которым пайпал будет авторизовывать нас при использовании api.

Далее нужно создать тестовый аккаунт для песочницы. Нажимаем ссылку [Sandbox accounts](https://developer.paypal.com/webapps/developer/applications/accounts) создаем тестового пользователя (под ним мы будем проводить тестовые оплаты). Сложностей тоже возникнуть не должно.

#### Шаг 2: Тестовое приложение

Устанавливаем SDK:

    Install-Package RestApiSDK

Создаем тестовое приложение (например, консольное приложение, хотя я использую пустой тест в проекте для этих целей, QuickTests). И копипастим в него код ниже, **предварительно заменив YOUR_CLIENT_ID и YOUR_CLIENT_SECRET на параметры нашего, только что созданного приложения.** Код, в принципе, можно взять из [Интерактивного гайда с примерами кода](https://devtools-paypal.com/guide/pay_paypal/dotnet?interactive=ON&env=sandbox), я его только собрал вместе и привел в приятный мне вид.
    
    var sdkConfig = new Dictionary<string, string> { { "mode", "sandbox" } };
    string accessToken = new OAuthTokenCredential("YOUR_CLIENT_ID", "YOUR_CLIENT_SECRET", sdkConfig)
                                .GetAccessToken();

    var redirectUrls = new RedirectUrls {
        cancel_url = "http://localhost:11180/PayPalResult?cancel=true",
        return_url = "http://localhost:11180/PayPalResult?success=true"
    };
    var amnt = new Amount { currency = "USD", total = "1" };
    var createdPayment = new Payment {
            intent = "sale",
            payer = new Payer { payment_method = "paypal" },
            transactions = new List<Transaction> {
                    new Transaction { description = "Sample payment", amount = amnt \}\},
            redirect_urls = redirectUrls}
        .Create(new APIContext(accessToken) { Config = sdkConfig });

    var approvalUrl = createdPayment.links.Single(l => l.rel == "approval_url").href;
    var paymentId = createdPayment.id;
    Console.WriteLine(approvalUrl);
    Console.WriteLine(paymentId);

На этом шаге нам нужны 2 значения: approvalUrl и paymentId. paymentId мы запоминаем на будущее, а по approvalUrl заходим в браузере.

Переходим по approvalUrl, логинимся под тестовым аккаунтом, подтверждаем платеж, нас перекидывает на http://localhost:11180/PayPalResult?success=true&token=EC-DSKFJDSKFJEO42M&PayerID=DFKJDFKLGJEOR (не важно, есть ли у вас вэбсервер, который обслуживает порт 11180).

Берем параметр PayerID из этого урла и вставляем его, вместе с PaymentId (мы его получили чуть раньше), в следующий код:

    string payerID = "YOUR_PAYER_ID";
    string paymentId = "YOUR_PAYMENT_ID";

    var sdkConfig = new Dictionary<string, string> { { "mode", "sandbox" } };
    string accessToken = new OAuthTokenCredential("YOUR_CLIENT_ID", "YOUR_CLIENT_SECRET", sdkConfig)
                                .GetAccessToken();
    var pymntExecution = new PaymentExecution { payer_id = payerID };
    var payment = new Payment { id = paymentId }
                      .Execute(new APIContext(accessToken) { Config = sdkConfig }, pymntExecution);

Тут для нас важен payment.status, который теперь получил значение "approved". Ура, тест пройден!

Документация говорит, что дальше мы должны сделать [Refund a sale (API reference)](https://developer.paypal.com/webapps/developer/docs/api/#refund-a-sale), но я, пока, не разбирался что это такое.


#### Шаг 3: Интегрируем в наше приложение

С интеграцией кода выше в приложение, теоретически, не должно быть проблем. Но все же они у меня были. Связана эта проблема была с запоминанием paymentId между двумя методами. Как раз запомнить paymentId не сложно, сложно понять какому из запомненных платежей принадлежит текущий запрос. Ведь paypal в resultUrl не указывает никаких данных кроме PayerID. А по PayerID получить paymentIdо никак не получиться. 

Можно хранить это значение в сессии и считать, что пользователь проводит только одну транзакцию за раз.

А можно [поступить хитрее](http://stackoverflow.com/a/18970771/983661). Можно сгенерировать id для оплаты и попросить PayPal включить этот id в ResultUrl. Вот так:

    var redirectUrls = new RedirectUrls {
        cancel_url = "http://localhost:11180/PayPalResult?cancel=true&InvoiceId={SOME_ID}",
        return_url = "http://localhost:11180/PayPalResult?success=true&InvoiceId={SOME_ID}"
    };

С помощью этого значения уже можно найти соответствующий paymentId. В принципе, можно в RedirectUrls сразу передать paymentId, но мне кажется это не секьюрно (хотя безопасник из меня так себе, может эти значения хорошо защищены и по ним ничего нельзя получить). 

#### Заключение

Вот и все. Не так уж и сложно, как изначально казалось. Надеюсь кому-то еще эта инструкция пригодиться.

У меня есть пару открытых вопросов по интеграции. Если вы можете на них ответить -- буду благодарен.

- Как использовать token, который PayPal передает в ResultUrl. Понятно, что его можно как-то использовать, чтобы удостовериться, что это точно PayPal, а не злоумышленник. Вопрос как.

- При оплате PayPal показывает пользователю только то, что мы ему передали. Т.е. если мы не передали сумму заказа, то пользователь ее не увидит. Для меня это выглядит странно. Может это особенности песочницы?

- Нужно разбираться с Refund. Похоже это важный шаг в оплате. Интересно, если не сделать refund, может ли пользователь отменить транзакцию? 

- Что делать, если пользователь оплатил, а потом отменил транзакцию (вроде PayPal это позволяет)? Придет ли cancel запрос на ResultUrl и каков срок отмены?


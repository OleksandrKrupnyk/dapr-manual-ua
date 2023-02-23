# Огляд прив'язок (Bindings overview)

**Огляд будівельного блоку API прив'язок** (**Overview of the bindings API building block**)

Використовуючи API прив'язок Dapr, ви можете запускати свій додаток за подіями, 
що надходять із зовнішніх систем, і взаємодіяти із зовнішніми системами. 
За допомогою API зв'язування ви можете:

(Using Dapr’s bindings API, you can trigger your app with events coming in from external systems and interface with external systems. With the bindings API, you can:)

- Уникайти складнощів підключення та опитування з систем обміну повідомленнями, таких як черги та шини повідомлень. (Avoid the complexities of connecting to and polling from messaging systems, such as queues and message buses.)
- Зосередьтеся на бізнес-логіці, а не на деталях реалізації взаємодії з системою. (Focus on business logic, instead of the implementation details of interacting with a system.)
- Зберігайте свій код вільним від SDK та бібліотек. (Keep your code free from SDKs or libraries.)
- Обробляти повторні спроби та відновлення після збоїв. (Handle retries and failure recovery.)
- Перемикання між прив'язками під час виконання. (Switch between bindings at runtime.)
- Створюйте портативні застосунки з налаштуванням прив'язок до конкретного середовища без внесення змін до коду.(Build portable applications with environment-specific bindings set-up and no required code changes.)

Наприклад, з прив'язками ваш мікросервіс може відповідати на вхідні повідомлення Twilio/SMS без них:
(For example, with bindings, your microservice can respond to incoming Twilio/SMS messages without:)

- Додавання або налаштування стороннього Twilio SDK (Adding or configuring a third-party Twilio SDK)
- Занепокоєння, щодо опитування з Twilio (або використання WebSockets тощо) (Worrying about polling from Twilio (or using WebSockets, etc.))


> **Примітка**
> 
> Прив'язки розробляються незалежно від часу виконання Dapr. Ви можете переглядати та долучатися до розробки прив'язок.

>(Note
> 
> Bindings are developed independently of Dapr runtime. You can view and contribute to the bindings.) 

## Вхідні прив'язування (Input bindings)

За допомогою прив'язок до входу ви можете запускати свій додаток, 
коли відбувається подія із зовнішнього ресурсу. 
Разом із запитом може надсилатися необов'язкове корисне 
навантаження та метадані.

(With input bindings, you can trigger your application when an event from an external resource occurs. An optional payload and metadata may be sent with the request.)

Щоб отримувати події від прив'язки входу (To receive events from an input binding:)

1. Визначте компонент YAML, який описує тип зв'язування та його метадані (інформація про з'єднання тощо).(Define the component YAML that describes the binding type and its metadata (connection info, etc.).)
2. Прослухайте вхідну подію за допомогою: (Listen for the incoming event using:)
   1. Кінцева точка HTTP (An HTTP endpoint)
   2. Прото-бібліотека gRPC для отримання вхідних подій. (The gRPC proto library to get incoming events.)

>Примітка
> 
> Під час запуску Dapr надсилає програмі запит `OPTIONS` для всіх 
> визначених прив'язок входу. 
> Якщо програма хоче підписатися на прив'язку, Dapr очікує код 
> стану `2xx` або `405`.

>Note
> 
> On startup, Dapr sends an `OPTIONS` request for all defined 
> input bindings to the application. If the application wants 
> to subscribe to the binding, Dapr expects a status code 
> of `2xx` or `405`.

(Read the Create an event-driven app using input bindings guide to get started with input bindings)


## Вихідні прив'язування (Output bindings)

За допомогою прив'язок виводу ви можете викликати зовнішні ресурси. 
Разом із запитом на виклик можна надсилати необов'язкове 
корисне навантаження та метадані.

(With output bindings, you can invoke external resources. An optional payload and metadata can be sent with the invocation request.)

Шоб викликати вихідне прив'язування: (To invoke an output binding:)

- Визначте компонент YAML, який описує тип зв'язування та його метадані (інформація про з'єднання тощо). (Define the component YAML that describes the binding type and its metadata (connection info, etc.).)
- Використовуйте кінцеву точку HTTP або метод gRPC для виклику прив'язки з необов'язковим корисним навантаженням. (Use the HTTP endpoint or gRPC method to invoke the binding with an optional payload.)

## Спробуйте прив'язки (Try out bindings)
### Короткі інструкції та навчальні посібники (Quickstarts and tutorials)

Хочете протестувати API прив'язок Dapr? Перегляньте наведені нижче інструкції та навчальні матеріали, щоб побачити прив'язки в дії:

(Want to put the Dapr bindings API to the test? Walk through the following quickstart and tutorials to see bindings in action:)

| Quickstart/tutorial | 	Description                                                                                                                                                                                                                                    |
|:--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Bindings quickstart](https://docs.dapr.io/getting-started/quickstarts/bindings-quickstart/) | 	Працюйте з зовнішніми системами, використовуючи вхідні зв'язки для реагування на події та вихідні зв'язки для виклику операцій. (Work with external systems using input bindings to respond to events and output bindings to call operations.) |
| [Bindings tutorial ](https://github.com/dapr/quickstarts/tree/master/tutorials/bindings)  | Демонструє, як використовувати Dapr для створення прив'язок вводу та виводу до інших компонентів. Використовує прив'язки до Kafka (Demonstrates how to use Dapr to create input and output bindings to other components. Uses bindings to Kafka)  |

### Почніть використовувати прив'язки безпосередньо у вашому додатку (Start using bindings directly in your app)

Хочете пропустити швидкий старт? Не проблема. 
Ви можете випробувати будівельний блок прив'язок безпосередньо 
у вашому додатку, щоб викликати прив'язки виводу і запускати 
прив'язки вводу. Після встановлення Dapr ви можете почати 
користуватися API прив'язок, починаючи з посібника з прив'язок вводу

(Want to skip the quickstarts? Not a problem. You can try out the bindings building block directly in your application to invoke output bindings and trigger input bindings. After Dapr is installed, you can begin using the bindings API starting with the input bindings how-to guide)
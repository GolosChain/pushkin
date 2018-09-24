# PUSH-SERVICE

**PUSH-SERVICE** является микросервисом рассылки push-уведомлений на мобильные устройства и браузеры пользователей [golos.io](https://golos.io).
Также хранит настройки пользователя, указывающие на необходимость рассылки конкретных типов уведомлений и их язык.

API JSON-RPC:

 ```
 transfer:                                     // Передача сообщения, отправляется с сервиса нотификаций
    user:       <string>                       // Имя пользователя
    data:       <{notifyType->[notifyEvent]}>  // Нотификации в виде объекта тип->массив_событий

 getOptions:                                   // Получение настроек
    key:        <string>                       // Уникальный ключ устройства

 setOptions:                                   // Установка настроек
    key:        <string>                       // Уникальный ключ устройства
    lang:       <'ru'|'en'|'ua'>               // Язык сообщений
    show:       <{notifyType->boolean}>        // Настройки отображения в виде тип->нужно_отображать
 ```

Возможные переменные окружения `ENV`:

 - `GLS_CONNECTOR_HOST` *(обязательно)* - адрес, который будет использован для входящих подключений связи микросервисов.
  Дефолтное значение при запуске без докера - `127.0.0.1`

 - `GLS_CONNECTOR_PORT` *(обязательно)* - адрес порта, который будет использован для входящих подключений связи микросервисов.
  Дефолтное значение при запуске без докера - `8080`

 - `GLS_METRICS_HOST` *(обязательно)* - адрес хоста для метрик StatsD.
  Дефолтное значение при запуске без докера - `127.0.0.1`

 - `GLS_METRICS_PORT` *(обязательно)* - адрес порта для метрик StatsD.
  Дефолтное значение при запуске без докера - `8125`

 - `GLS_MONGO_CONNECT` - строка подключения к базе MongoDB.
  Дефолтное значение - `mongodb://mongo/admin`

 - `GLS_DAY_START` - время начала нового дня в часах относительно UTC.
  Дефолтное значение - `3` (день начинается в 00:00 по Москве).
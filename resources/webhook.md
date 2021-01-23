---
description: >-
  Вебхуки - более простой способ для отправки сообщений в каналы. Они не требуют
  какой либо авторизации.
---

# Вебхук

## Объект вебхука <a id="webhook-object"></a>

Нужен для представления вебхука.

### Структура вебхука <a id="webhook-object-webhook-structure"></a>

| Поле | Тип | Описание |
| :--- | :--- | :--- |
| id | snowflake | ID вебхука |
| type | целое число | тип вебхука |
| guild\_id? | snowflake | ID сервера вебхука |
| channel\_id | snowflake | ID канала вебхука |
| user? | [пользователь](user.md) | пользователь, который создал вебхук. не возвращается при попытки получить вебхук по его токену |
| name | строка | имя вебхука по умолчанию |
| avatar | строка | URL аватара по умолчанию |
| token? | строка | токен вебхука, только для первого типа |
| application\_id | snowflake | ID бота/OAuth2 приложения, которые создало вебхук |

### Типы вебхуков <a id="webhook-object-webhook-types"></a>

| Значение | Имя | Описание |
| :--- | :--- | :--- |
| 1 | Входящий | Входящие вебхуки могут отправлять сообщения с сгенерированным токеном  |
| 2 | Подписка на канал | Новости с подписанных каналов приходят с помощью функции подписки на новостные каналы |

### Пример вебхука <a id="webhook-object-example-webhook"></a>

```javascript
{
  "name": "тест",
  "type": 1,
  "channel_id": "199737254929760256",
  "token": "3d89bb7572e0fb30d8128367b3b1b44fecd1726de135cbe28a41f8b2f777c372ba2939e72279b94526ff5d1bd4358d65cf11",
  "avatar": null,
  "guild_id": "199737254929760256",
  "id": "223704706495545344",
  "user": {
    "username": "SNVMK",
    "discriminator": "6001",
    "id": "190320984123768832",
    "avatar": "b004ec1740a63ca06ae2e14c5cee11f3"
  }
}
```

{% api-method method="post" host="" path="/channels/:id/webhooks" %}
{% api-method-summary %}
Создать вебхук
{% endapi-method-summary %}

{% api-method-description %}
Создаёт новый вебхук. Требует разрешения управления вебхуками. Возвращает объект вебхука, при удачном выполнении.  
`name` не может быть **Clyde**
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="avatar" type="object" required=false %}
Аватар вебхука
{% endapi-method-parameter %}

{% api-method-parameter name="name" type="string" required=false %}
Имя вебхука
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}
Возвращает объект вебхука
{% endapi-method-response-example-description %}

```
{
    <webhook object>
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Отправлен неправильный запрос
{% endapi-method-response-example-description %}

```
{"message": "The request was improperly formatted, or the server couldn't understand it.", "code": 0}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="" path="/channels/:id/webhooks" %}
{% api-method-summary %}
Получить вебхуки канала
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}
Возвращает список из объектов вебхука
{% endapi-method-response-example-description %}

```
[
    {
    <webhook object>
    },
    {
    <webhook object 2>
    },
    ...,
    {
    <webhook object N>
    }
]
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{"message": "Unknown channel", "code": 10003}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}


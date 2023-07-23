# Migration guide

## [V3](https://github.com/getCompass/userbot/blob/master/README_ru.md)

Руководство по миграции с версии V2 до версии V3 Userbot API.<br>
Добавлены следующие изменения для Userbot API:
  - Все запросы в Userbot API выполняются синхронно и сразу возвращают результат своего выполнения.
  - Удалён API-метод /request/get.
  - Изменён способ авторизации запросов к Userbot API - header-заголовок Signature удалён из проекта. Теперь для авторизации запроса необходимо передавать только header-заголовок Authorization.
  - Изменился список системных ошибок - удалена ошибка "Некорректная подпись для валидации переданных данных".
  - Запрос, отправляемый на webhook, теперь содержит только header-заголовок Authorization.
  - Добавилась возможность синхронного ответа на запрос, пришедший на ваш webhook. 

**Инструкция для миграции Userbot API:**
1) Поправьте все запросы к Userbot API, указав в URL запроса новую версию API (версия 3).<br>
Было: <br>
`https://userbot.getcompass.com/api/v2/user/send` <br>
Стало: <br>
`https://userbot.getcompass.com/api/v3/user/send` <br>

2) Удалите использование метода /request/get.

3) Все методы из [Списка методов Compass Userbot API](https://github.com/getCompass/userbot/blob/master/README_ru.md#Список-методов-Compass-Userbot-API) теперь сразу возвращают результат своего выполнения.<br>
Замените получение request_id для методов на тот ответ, который ожидается в случае успешного выполнения запроса.

4) Удалите передачу заголовка Signature для запросов к V3 Userbot API.<br>
Теперь для валидации запроса необходимо передавать один header-заголовок:<br>
заголовок **"Authorization: bearer={токен бота}"** содержит токен вашего бота. 

5) Удалите для V3 Userbot API обработку системной ошибки, которая имеет error_code = 4.

**Инструкция для миграции webhook:**
1) С помощью метода [webhook/setVersion](https://github.com/getCompass/userbot/blob/master/README_ru.md#post-webhooksetversion) установите новую версию (версия 3) webhook для своего бота.

2) В вашем проекте, где обрабатывается запрос, пришедший на ваш webhook, удалите обработку заголовка Signature.


## [V2](https://github.com/getCompass/userbot/releases/tag/v2)

Руководство по миграции с релизной версии до версии V2 Userbot API.<br>
Добавлены следующие изменения:
- Добавлена новая версия Userbot API (версия 2).
- Изменён способ авторизации запросов к Userbot API - теперь для авторизации запросов используются header-заголовки.
- Изменён формат параметра user_id: ранее используемый как "User-{ID}", теперь он принимает int-значение.
- На URL-адрес установленного webhook параметр user_id также передаётся в формате int-значения.
- Добавлены новые API-методы: [webhook/setVersion](https://github.com/getCompass/userbot#post-webhooksetversion) и [webhook/getVersion](https://github.com/getCompass/userbot/blob/master/README_ru.md#post-webhookgetversion).

Инструкция для миграции:
1) Поправьте все запросы к Userbot API, указав в URL запроса новую версию API.<br>
Было: <br>
`https://userbot.getcompass.com/api/v1/user/send` <br>
Стало: <br>
`https://userbot.getcompass.com/api/v2/user/send` <br>
   
2) Запросы к V2 Userbot API должны иметь header-заголовки:
    - заголовок **"Authorization: bearer={токен бота}"** содержит токен вашего бота;
    - заголовок **"Signature: signature={подпись запроса}"** - подпись для валидации данных запроса.

3) В методах [user/send](https://github.com/getCompass/userbot/blob/master/README_ru.md#post-usersend), [user/getList](https://github.com/getCompass/userbot/blob/master/README_ru.md#post-usergetlist) параметр `user_id` имеет формат int-значения.<br>
Префикс "User-" был удалён.<br>
>Пример:
>```json5 
>{
>   "user_id": 12345
>}
>```

   
4) При отправке запроса на установленный webhook user_id имеет формат int-значения.<br>
Префикс "User-" был удалён.<br>
> Пример отправлямых на webhook данных:
>```json5 
>{
>     "group_id": "",
>     "message_id": "oDT9FLRWjDOX0+4smgkCn039jKIce+NUE90zy9neDKvh6ubLMDGU/Cee5e07avTPFT/WcnAJIX...",
>     "text": "/покажи список команд"
>     "type": "single",
>     "user_id": 12345,
>}
>```

5) Для возможности смены версии webhook вашего бота используйте новые методы Userbot API:
    - [webhook/setVersion](https://github.com/getCompass/userbot/blob/master/README_ru.md#post-webhooksetversion)
    - [webhook/getVersion](https://github.com/getCompass/userbot/blob/master/README_ru.md#post-webhookgetversion)


## [Userbot release](https://github.com/getCompass/userbot/releases/tag/v1)

- Реализованы чат-боты Compass.

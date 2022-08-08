# Changelog

## [Api V2](https://github.com/getCompass/userbot/releases/tag/master)

- Добавлена новая версия Userbot API (версия 2).
- Реализован новый способ авторизации запросов к Userbot API.
- Изменён формат параметра user_id: ранее используемый как "User-{ID}" теперь принимает int-значение.
- На URL-адрес установленного webhook параметр user_id также передаётся в формате int-значения.
- Добавлены новые API-методы: [webhook/setVersion](https://github.com/getCompass/userbot#post-webhooksetversion) и [webhook/getVersion](https://github.com/getCompass/userbot#post-webhookgetversion).

## [Userbot release](https://github.com/getCompass/userbot/releases/tag/v1)

- Реализованы чат-боты Compass.

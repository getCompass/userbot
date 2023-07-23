[![en](https://img.shields.io/badge/lang-en-green.svg)](https://github.com/getCompass/userbot/blob/master/CHANGELOG.md)
[![ru](https://img.shields.io/badge/lang-ru-green.svg)](https://github.com/getCompass/userbot/blob/master/CHANGELOG_ru.md)

# Changelog

## [Api V3](https://github.com/getCompass/userbot/releases/tag/master)

- A new version of the Userbot API (version 3) has been added
- All requests to the Userbot API are executed synchronously and immediately return the result of their execution
- The /request/get API method has been removed
- The request authorization method for the Userbot API has been changed: the Signature header has been removed from the project. Now only the Authorization header must be sent to authorize the request
- The list of system errors has changed: the error "Incorrect signature for validation of transmitted data" has been removed
- The request sent to the webhook now contains only the Authorization header
- An option to synchronously respond to a request coming to your webhook has been added

## [Api V2](https://github.com/getCompass/userbot/releases/tag/v2)

- A new version of the Userbot API (version 2) has been added
- A new way to authorize requests to the Userbot API has been implemented
- The format of the user_id parameter has been changed: previously used as "User-{ID}", now it takes an int value
- The user_id parameter is also passed to the URL of the installed webhook in int-value format
- The new API methods have been added: [webhook/setVersion](https://github.com/getCompass/userbot#post-webhooksetversion) и [webhook/getVersion](https://github.com/getCompass/userbot#post-webhookgetversion)

## [Userbot release](https://github.com/getCompass/userbot/releases/tag/v1)

- Compass bots have been implemented

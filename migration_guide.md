# Migration guide

## [V3](https://github.com/getCompass/userbot)

A guide to migrating from version V2 to version V3 of the Userbot API.<br>
The following changes have been added for the Userbot API:
  - All requests to the Userbot API are executed synchronously and immediately return the result of their execution
  - The /request/get API method has been removed
  - The request authorization method for the Userbot API has been changed: the Signature header has been removed from the project. Now only the Authorization header must be sent to authorize the request
  - The list of system errors has changed: the error "Incorrect signature for validation of transmitted data" has been removed
  - The request sent to the webhook now contains only the Authorization header
  - An option to synchronously respond to a request coming to your webhook has been added

**Instructions for migrating the Userbot API:**
1) Correct all requests to the Userbot API by specifying the new API version (version 3) in the request URL.<br>
Before: <br>
`https://userbot.getcompass.com/api/v2/user/send` <br>
After: <br>
`https://userbot.getcompass.com/api/v3/user/send` <br>

2) Remove the use of the /request/get method.

3) All methods from the [Compass Userbot API methods](https://github.com/getCompass/userbot#Compass-Userbot-API-method-list) list now immediately return the result of their execution.<br>
Replace getting the request_id for the methods with the response that is expected if the request is successful.

4) Remove the Signature header transmission for requests to the V3 Userbot API.<br>
Now, to validate the request, you need to pass one header:<br>
the header **"Authorization: bearer={bot token}"** contains your bot's token. 

5) Remove the system error handling for the V3 Userbot API, which has error_code = 4.

**Instructions for webhook migration:**
1) Use the [webhook/setVersion](https://github.com/getCompass/userbot#post-webhooksetversion) method to install a new version (version 3) of the webhook for your bot.

2) In your project, where the request that came to your webhook is processed, remove the Signature header processing.


## [V2](https://github.com/getCompass/userbot/releases/tag/v2)

A guide to migrating from the release version to the version V2 Userbot API.<br>
The following changes have been added:
- A new version of the Userbot API (version 2) has been added
- The request authorization method for the Userbot API has been changed: the headers are now used for authorization of requests
- The format of the user_id parameter has been changed: previously used as "User-{ID}", now it takes an int value
- The user_id parameter is also passed to the URL of the installed webhook in int-value format
- The new API methods have been added: [webhook/setVersion](https://github.com/getCompass/userbot#post-webhooksetversion) и [webhook/getVersion](https://github.com/getCompass/userbot#post-webhookgetversion)

Instructions for migration:
1) Correct all requests to the Userbot API by specifying the new API version in the request URL.<br>
Before: <br>
`https://userbot.getcompass.com/api/v1/user/send` <br>
After: <br>
`https://userbot.getcompass.com/api/v2/user/send` <br>
   
2) Requests to the V2 Userbot API must have headers:
    - the header **"Authorization: bearer={bot token}"** contains your bot token
    - the header **"Signature: signature=< signature request >"** is a signature for validating the request data

3) In [user/send](https://github.com/getCompass/userbot#post-usersend), [user/getList](https://github.com/getCompass/userbot#post-usergetlist) methods, the `user_id` parameter has the int-value format.<br>
The prefix "User-" has been removed.<br>
>Example:
>```json5 
>{
>   "user_id": 12345
>}
>```

   
4) When sending a request to the installed webhook, the user_id has the int-value format.<br>
The prefix "User-" has been removed.<br>
> Example of data sent to the webhook:
>```json5 
>{
>     "group_id": "",
>     "message_id": "oDT9FLRWjDOX0+4smgkCn039jKIce+NUE90zy9neDKvh6ubLMDGU/Cee5e07avTPFT/WcnAJIX...",
>     "text": "/show command list"
>     "type": "single",
>     "user_id": 12345,
>}
>```

5) To be able to change the webhook version of your bot, use the new methods of the Userbot API:
    - [webhook/setVersion](https://github.com/getCompass/userbot#post-webhooksetversion)
    - [webhook/getVersion](https://github.com/getCompass/userbot#post-webhookgetversion)


## [Userbot release](https://github.com/getCompass/userbot/releases/tag/v1)

- Compass bots have been implemented

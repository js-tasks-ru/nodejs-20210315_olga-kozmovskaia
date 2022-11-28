# Чат с использованием Websockets

В этой задаче вам потребуется реализовать функциональность чата с использованием технологии 
Websockets. Задача состоит из нескольких подзадач:


1. Реализовать аутентификацию по токену для подключений по Websockets:
   - пользователь передаёт токен в параметре `token` запроса
   - если параметра `token` нет - необходимо вернуть ошибку 
   `new Error("anonymous sessions are not allowed")`
   - если сессии по переданному токену нет - необходимо вернуть ошибку
   `new Error("wrong or expired session token")`
   - объект пользователя необходимо записать в свойство `socket.user` (это нужно для следующей
   подзадачи)  
2. На каждое сообщения пользователя, пришедшее по протоколу Websocket (событие `message`) 
   необходимо сохранять сообщение в базу, передав 4 значения:
   - `date` - текущая дата
   - `text` - текст сообщения
   - `chat` - идентификатор чата, являющийся идентификатором текущего пользователя (т.е. `user.id`)
   - `user` - имя (`displayName` пользователя) 
3. Реализовать получение истории сообщений по адресу `GET /messages`. Этот эндпойнт должен быть
доступен лишь аутентифицированным пользователям и возвращать сообщения предназначенные для текущего пользователя. Нет необходимости возвращать все сообщения сразу, достаточно будет лишь последних 20. Формат каждого объекта сообщения следующий:
```js
{
    date: Date, // дата сообщения
    text: String, // текст сообщения
    id: String, // идентификатор сообщения
    user: String, // Имя (displayName) пользователя, отправившего это сообщение
}
```
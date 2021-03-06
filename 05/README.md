# Комментарии к 05:Guestbook

____


## Логика ACCESS_LEVEL

1 - admin (главный администратор)

Видит IP-адресса, может удалять любые сообщения

2 - authorized_user (авторизованный пользователь)

Не видит IP-адресса, может удалять сообщения, отправленные им

3 - guest (гость)

Не видит IP-адресса, не может удалять никакие сообщения

## Информация о пользователях

admin => root (access_level = 1)

misha => smd (access_level = 2)

## Хранение сообщений в $messagesArr

$messagesArr имеет следующую структуру и хранит в себе все сообщения:

```
[
    [message_id] => [
        'username'     => Имя пользователя,
        'datetime'     => Дата и время отправки сообщения,
        'message_text' => Текст отправленного сообщения,
        'user_ip'      => IP-адресс клиента
    ]

    [message_id] => [
        ...
    ]

    .....
]
```

## Комментарий об удалении сообщений

Логично заявить, если критерием для удаления сообщений будет являться совпадение IP-адресса
с которого было отправлено сообщение с IP-адрессом клиента, который хочет его удалить.

Однако, поскольку гостевая книга была реализована в рамках учебного проекта и все время запускается на локальном сервере
в качестве критерия было выбрано совпадение username'ов: того, кто отправил сообщение и того, кто хочет удалить его.

Вследствие чего образовывается некий **баг**:
Если некий гость будет оставлять сообщения в книге под ником qwerty, то любой другой
пользователь, зарегистрировавшись под ником qwerty, сможет удалить сообщения гостя.

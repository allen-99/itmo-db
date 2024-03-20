```
CREATE TABLE users (
    userId SERIAL PRIMARY KEY,
    userName VARCHAR(100) NOT NULL,
    userEmail VARCHAR(255) UNIQUE NOT NULL,
    userPassword VARCHAR(255) NOT NULL
);


INSERT INTO users (userName, userEmail, userPassword)
VALUES
    ('Иван Иванов', 'ivan@example.com', 'пароль_ивана'),
    ('Елена Смирнова', 'elena@example.com', 'пароль_елены'),
    ('Александр Петров', 'alex@example.com', 'пароль_александра'),
    ('Мария Васильева', 'maria@example.com', 'пароль_марии'),
    ('Сергей Кузнецов', 'sergey@example.com', 'пароль_сергея');


CREATE TABLE chat (
    chatId SERIAL PRIMARY KEY,
    chatName VARCHAR(100) NOT NULL,
    firstUserId INT NOT NULL,
    secondUserId INT NOT NULL,
    FOREIGN KEY (firstUserId) REFERENCES users(userId),
    FOREIGN KEY (secondUserId) REFERENCES users(userId)
);

INSERT INTO chat (chatName, firstUserId, secondUserId)
VALUES
    ('Первый чат', 1, 2),
    ('Второй чат', 3, 4),
    ('Третий чат', 2, 5);

SELECT * FROM users;
SELECT * FROM chat;

CREATE TABLE messages (
    messageId SERIAL PRIMARY KEY,
    lastMessageId SERIAL,
    lastMessageText TEXT,
    chatId INT NOT NULL,
    userId INT NOT NULL,
    FOREIGN KEY (chatId) REFERENCES chat(chatId),
    FOREIGN KEY (userId) REFERENCES users(userId)
);

INSERT INTO messages (lastMessageText, chatId, userId)
VALUES
    ('Привет, как дела?', 1, 1),
    ('Всё отлично, спасибо!', 1, 2),
    ('Какой план на выходные?', 2, 3),
    ('Думаю, сходить в кино.', 2, 4),
    ('Кто-нибудь хочет присоединиться?', 3, 2),
    ('Я бы с удовольствием!', 3, 5);

SELECT * FROM messages;

SELECT
    u.userId, u.userName, u.userEmail,
    c.chatId, c.chatName,
    MAX(m.messageId) AS lastMessageId,
    MAX(m.lastMessageText) AS lastMessageText
FROM
    users u
JOIN
    chat c ON u.userId = c.firstUserId OR u.userId = c.secondUserId
JOIN
    messages m ON c.chatId = m.chatId
GROUP BY
    u.userId, u.userName, u.userEmail, c.chatId, c.chatName
ORDER BY
    c.chatId, lastMessageId;

```

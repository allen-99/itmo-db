```
db.createCollection("users")

db.users.insertMany([
  { login: "user1", name: "Иван Иванов", password: "password1" },
  { login: "user2", name: "Елена Смирнова", password: "password2" },
  { login: "user3", name: "Алексей Петров", password: "password3" }
])

db.createCollection("messages")

db.messages.insertMany([
  { login: "user1", messageText: "Привет, как дела?" },
  { login: "user2", messageText: "Всё отлично, спасибо!" },
  { login: "user3", messageText: "Какой план на выходные?" }
])
```

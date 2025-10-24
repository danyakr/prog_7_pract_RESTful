# Практическая работа - RESTful веб-приложение на Spring Boot

## Цель работы
Создать RESTful веб-приложение “Task Management System” для управления задачами с использованием Spring Boot, применяя ключевые компоненты фреймворка, включая автоматическую конфигурацию, стартеры,
работу с базой данных и безопасность.


### 1. Проверка без аутентификации

**Запрос:**
```
GET http://localhost:8080/api/tasks
```

**Авторизация:** No Auth (Без аутентификации)

**Ожидаемый результат:** Статус `401 Unauthorized`

![Проверка без аутентификации](https://github.com/user-attachments/assets/53043e42-653e-4d20-be6b-858e032a386d)

---

### 2. Проверка с базовой аутентификацией

**Запрос:**
```
GET http://localhost:8080/api/tasks
```

**Авторизация:** Basic Auth
- **Username:** `admin`
- **Password:** `admin123`

**Ожидаемый результат:** Статус `200 OK` и пустой массив `[]` (или список созданных задач)

![Проверка с базовой аутентификацией](https://github.com/user-attachments/assets/2197243d-789e-478c-90c6-561cc046800c)

---

## Проверка CRUD-операций

### CREATE - Создание задачи

**Запрос:**
```
POST http://localhost:8080/api/tasks
```

**Body:** (raw, JSON)
```json
{
  "title": "Test Task",
  "description": "Desc",
  "status": "Pending"
}
```

**Ожидаемый результат:** Статус `200 OK`, в ответе будет `"id": 1`

![Создание задачи](https://github.com/user-attachments/assets/e0a64736-d721-4391-b928-4a47418535fc)

---

### READ - Чтение одной задачи

**Запрос:**
```
GET http://localhost:8080/api/tasks/1
```

**Ожидаемый результат:** Статус `200 OK` с полными данными задачи ID 1

![Чтение задачи](https://github.com/user-attachments/assets/d036e35e-9ab8-40e8-80c7-5480396a40f0)

---

### UPDATE - Обновление задачи

**Запрос:**
```
PUT http://localhost:8080/api/tasks/1
```

**Body:** (raw, JSON)
```json
{
  "title": "Test Task",
  "description": "Desc",
  "status": "Completed"
}
```

**Ожидаемый результат:** Статус `200 OK` с обновленным объектом

![Обновление задачи](https://github.com/user-attachments/assets/e83179b3-2f00-4579-a5a9-05da4f419876)

---

### Ошибка 404 - Несуществующая задача

**Запрос:**
```
GET http://localhost:8080/api/tasks/11
```

**Ожидаемый результат:** Статус `404 Not Found` (это подтверждает, что обработчик исключений работает)

![Ошибка 404](https://github.com/user-attachments/assets/510687da-81fc-4a3e-adfe-26c227a0bee2)

---

### DELETE - Удаление задачи

**Запрос:**
```
DELETE http://localhost:8080/api/tasks/1
```

**Ожидаемый результат:** Статус `200 OK` (задача удалена)

![Удаление задачи](https://github.com/user-attachments/assets/97623952-268c-40d2-9bb5-6e22cb4c2435)

---

## Проверка Базы Данных (H2 Console)

### Доступ к H2 Console

1. Откройте браузер
2. Перейдите на `http://localhost:8080/h2-console`
3. Подключитесь, используя настройки из `application.yml`
   - **JDBC URL:** `jdbc:h2:mem:taskdb`

---

### Создание Записи Напрямую в Базе (INSERT)

```sql
INSERT INTO TASK (TITLE, DESCRIPTION, STATUS, CREATED_AT)
VALUES ('title', 'description', 'status', NOW());
```

![Создание записи в базе данных](https://github.com/user-attachments/assets/f6ea798a-4f9c-4bb2-8614-22a3383c6c44)

---

### Просмотр Внесенных Данных (SELECT)

```sql
SELECT * FROM TASK;
```

**Ожидаемый результат:** Отображение всех записей из таблицы tasks, включая только что созданную запись

![Просмотр данных в базе](https://github.com/user-attachments/assets/e36ce91e-d01d-4217-aac5-d807baa969b2)

---

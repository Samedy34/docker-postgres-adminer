# PostgreSQL + Adminer (Docker Compose)

Развёртывание PostgreSQL и Adminer через Docker Compose на VPS.

## 📦 Состав

- **PostgreSQL 16** — реляционная СУБД.
- **Adminer** — простой веб-интерфейс для управления базой данных.

---

## 📁 Структура проекта

```
project-root/
├── docker-compose.yml
├── .env
└── README.md
```

---

## 🚀 Быстрый старт

### 1. Клонируй или скопируй репозиторий

```bash
git clone <URL> postgres-adminer
cd postgres-adminer
```

### 2. Создай `.env` файл

```env
# .env

POSTGRES_DB=mydatabase
POSTGRES_USER=myuser
POSTGRES_PASSWORD=mypassword
POSTGRES_PORT=5432

ADMINER_PORT=8080
```

### 3. Запусти контейнеры

```bash
cp .env.example .env
```
Настрой

```bash
docker compose up -d
```

---

## 🌐 Доступ

- **Adminer:** http://<IP_вашего_VPS>:8080  
- **PostgreSQL:** порт `5432` (или тот, что указали в `.env`)

### Данные для входа в Adminer:

- **System:** PostgreSQL  
- **Server:** `postgres`  
- **Username:** `myuser`  
- **Password:** `mypassword`  
- **Database:** `mydatabase`

---

## 🐳 docker-compose.yml

```yaml
version: '3.8'

services:
  postgres:
    image: postgres:16
    container_name: postgres
    restart: always
    environment:
      POSTGRES_DB: ${POSTGRES_DB}
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
    volumes:
      - postgres_data:/var/lib/postgresql/data
    ports:
      - "${POSTGRES_PORT}:5432"

  adminer:
    image: adminer
    container_name: adminer
    restart: always
    ports:
      - "${ADMINER_PORT}:8080"

volumes:
  postgres_data:
```

---

## 🛠 Полезные команды

```bash
# Остановить контейнеры
docker compose down

# Просмотреть логи
docker compose logs -f

# Перезапустить
docker compose restart
```

---

## 🔐 Безопасность

- **Пароли:** не используйте слабые пароли в `.env`.
- **Adminer:** ограничьте доступ к `8080` через UFW или Nginx.
- **PostgreSQL:** по возможности, не открывайте порт наружу (`5432`), используйте внутреннюю сеть Docker или VPN.

---

## 🧼 Лицензия

MIT

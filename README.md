# HackPrimeCode — Deploy

## Быстрый старт

### 1. Клонировать репозиторий вместе с сабмодулями

```bash
git clone --recurse-submodules https://github.com/HackPrimeCode/deploy
cd deploy
```

Если уже склонировали без флага:

```bash
git submodule update --init --recursive
```

### 2. Создать `.env` файлы

```bash
cp ML/.env.example ML/.env
```

> Backend — добавьте `.env` по аналогии, если у него есть `.env.example`.

### 3. Заполнить переменные окружения

Откройте `ML/.env` и укажите свои ключи:

```env
GITHUB_TOKEN=ghp_...
OPENROUTER_API_KEY=sk-or-v1-...
```

Создайте `.env` в корне для параметров базы данных и MinIO (или оставьте дефолтные значения из `docker-compose.yml`):

```bash
# .env (в корне, рядом с docker-compose.yml)
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
POSTGRES_DB=hackprimecode

MINIO_ROOT_USER=minioadmin
MINIO_ROOT_PASSWORD=minioadmin
```

### 4. Запустить

```bash
docker compose up --build -d
```

Приложение будет доступно на [http://localhost](http://localhost).

| Сервис       | URL                          |
|--------------|------------------------------|
| Фронтенд     | http://localhost             |
| Backend API  | http://localhost/api/        |
| ML API       | http://localhost/ml/api/     |
| MinIO консоль| http://localhost:9001        |

### 5. Остановить

```bash
docker compose down
```

Чтобы также удалить данные баз:

```bash
docker compose down -v
```

## Обновить сабмодули до последних коммитов

```bash
git submodule update --remote --merge
git add Backend Frontend ML
git commit -m "update submodules"
```

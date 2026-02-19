# Effective Mobile — DevOps тестовое задание

Python HTTP-сервер, проксируемый через Nginx. Всё запускается в Docker-контейнерах через Docker Compose.

## Содержание

- [Архитектура](#архитектура)
- [Стек](#стек)
- [Требования](#требования)
- [Запуск](#запуск)
- [Проверка](#проверка)
- [Структура проекта](#структура-проекта)
- [Остановка](#остановка)

## Архитектура

![Architecture](Architecture/architecture.svg)

Nginx принимает запросы снаружи и проксирует их на backend по имени сервиса внутри изолированной Docker-сети `effective_net`. Порт backend на хост не пробрасывается.

## Стек

| Компонент | Технология          |
|-----------|---------------------|
| Backend   | Python 3.12 slim    |
| Proxy     | Nginx Alpine        |
| Оркестрация | Docker Compose    |
| Сеть      | Docker bridge network |

## Требования

- Docker
- Docker Compose

## Запуск

**1. Клонировать репозиторий**

```bash
git clone <repo_url>
cd <repo_folder>
```

**2. Создать файл окружения**

```bash
cp .env.example .env
```

**3. Поднять контейнеры**

```bash
docker compose up --build -d
```

**4. Убедиться, что сервисы запустились**

```bash
docker compose ps
```

Оба контейнера должны быть в статусе `healthy`.

## Проверка

Основной запрос через Nginx:

```bash
curl http://localhost
```

Ожидаемый ответ:

```
Hello from Effective Mobile!
```

Проверка сетевой изоляции — backend не должен быть доступен напрямую:

```bash
curl http://localhost:8080
# Connection refused
```

## Структура проекта

```
├── Architecture/
│   └── architecture.svg
├── backend/
│   ├── Dockerfile
│   └── app.py
├── nginx/
│   └── nginx.conf
├── docker-compose.yml
├── .env.example
├── .gitignore
└── README.md
```

## Остановка

```bash
docker compose down
```

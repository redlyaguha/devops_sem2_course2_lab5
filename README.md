# Лабораторная работа 5 — CI/CD Pipeline (GitHub Actions)

## Описание
FastAPI API для управления пользователями с настроенным CI/CD пайплайном через GitHub Actions.

## Стек
- **Python 3.11**
- **FastAPI** + **Uvicorn**
- **Pydantic** — валидация данных
- **Pytest** + **httpx** — тестирование
- **GitHub Actions** — CI/CD
- **Docker** — контейнеризация

## API Эндпоинты

| Метод | Путь | Описание |
|-------|------|----------|
| `GET` | `/api/v1/user?email=` | Получить пользователя по email |
| `POST` | `/api/v1/user` | Создать пользователя (с проверкой на дубликаты) |
| `DELETE` | `/api/v1/user?email=` | Удалить пользователя по email |

## Структура
```
├── src/
│   ├── main.py              # Точка входа FastAPI
│   ├── routers/user.py      # API эндпоинты
│   ├── schemas/user.py      # Pydantic модели
│   ├── fake_db/database.py  # In-memory "база данных"
│   └── settings.py          # Настройки приложения
├── tests/
│   └── test_user.py         # 5 тестов (pytest)
├── .github/workflows/
│   ├── tests.yml            # CI: запуск тестов при каждом push
│   └── build-and-delivery.yml  # CD: сборка и публикация Docker образа
├── Dockerfile
└── requirements.txt
```

## CI/CD Пайплайн

### 1. Tests (tests.yml)
- Запускается при каждом push
- Устанавливает зависимости
- Запускает pytest

### 2. Build & Delivery (build-and-delivery.yml)
- Запускается при успешных тестах в main ветку
- Собирает Docker образ
- Публикует в Docker Hub

## Запуск локально

```bash
pip install -r requirements.txt
uvicorn src.main:app --reload
```

## Тесты

```bash
pytest tests/
```

## Docker

```bash
docker build -t user-api .
docker run -p 8000:8000 user-api
```

## Проделанная работа
- Разработан FastAPI API с in-memory базой данных
- Написан набор из 5 unit-тестов с использованием pytest и httpx
- Настроен CI-пайплайн в GitHub Actions для автоматического запуска тестов
- Настроен CD-пайплайн для автоматической сборки и публикации Docker образа в Docker Hub
- Создан Dockerfile для контейнеризации приложения

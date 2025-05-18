# Taski - приложение для планирования задач.

## Стек технологий
`Python` `YAML` `Django` `Django REST Framework` `Djoser` `API` `Nginx` `Docker` `PostgreSQL` `Gunicorn` `Postman` `GitHub Actions(CI/CD)`

## Локальный запуск с Docker

**Клонировать репозиторий**
```bash
git clone git@github.com:okhotinaks/taski-docker.git
```
```bash
cd taski-docker
```
**Создать виртуальное окружение**
```bash
python -m venv venv
```
```bash
source venv/bin/activate
```
**Установить зависимости из файла requirements.txt**
```bash
python3 -m pip install --upgrade pip
```
```bash
cd backend
```
```bash
pip install -r requirements.txt
```
**Создать файл .env (в корневой директории) в соответствии с примером .env.example**
```bash
cd ..
```
```bash
touch .env
```
**Запустить контейнеры**
```bash
docker compose up --build
```
**Создаем и применяем миграции**
```bash
docker compose exec backend python manage.py makemigrations
```
```bash
docker compose exec backend python manage.py migrate
```
**Сборка статики**
```bash
docker compose exec backend python manage.py collectstatic
docker compose exec backend cp -r /app/collected_static/. /backend_static/static/
``` 
**Проект доступен по адресу:**
http://localhost:8000/

## Автоматическое развертывание (CI/CD)
Настроен деплой на сервер через GitHub Actions.
После каждого обновления репозитория (при пуше в ветку main) будет происходить:
- Проверка кода на соответсвие стандарту PEP8(с помощью пакета flake8)
- Сборка и отправка докер-образов на Docker Hub: frontend, backend, gateway
- Разворачивание проекта на удаленном сервере
- Применение миграций, сборка статики
- Отправка сообщения в Telegram в случае успеха

**Автор проекта:**
Охотина Ксения Николаевна - [github.com/okhotinaks](https://github.com/okhotinaks)


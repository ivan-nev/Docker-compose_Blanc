
### Пустая заготовка Docker-compose:

Конфигурация состоит из 3-х контейнеров: backend, postgres, nginx. 

Контейнеры объединяются в сеть, которые работают в связке:

- Nginx работает в качестве proxy-http для пересылки динамических запросов к Django или возвращая статические html файлы.
- PostgreSQL запускается до Django.
- Django запускается через Gunicorn.

после скачивания репозитория необходимо обновить права для файлов
- $ chmod +x app/entrypoint.prod.sh
- $ chmod +x app/entrypoint.sh

Остановка контейнера
- $ docker-compose down -v

Запуск контейнерa продакшн
- $ docker-compose -f docker-compose.prod.yml up -d --build
- $ docker-compose -f docker-compose.prod.yml exec web python manage.py migrate --noinput
- $ docker-compose -f docker-compose.prod.yml exec web python manage.py collectstatic --no-input --clear
- http://host/admin/
- http://host/

Запуск контейнера разработки без ngix (база очищается, все изменения в папке app передаются сразу в контейнер)
- $ docker-compose -f docker-compose.yml up -d --build
- http://localhost:8000/admin/
- http://localhost:8000/
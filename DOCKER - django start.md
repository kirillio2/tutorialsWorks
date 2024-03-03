# DOCKER - django start

Dockerfile:
FROM python:3
WORKDIR /usr/src/app
COPY requirements.txt ./
RUN pip install -r requirements.txt

requirements.txt:
Django>=3.0,<4.0
psycopg2-binary>=2.8

docker-compose.yml:
version: '3'

services:
  django:
    build: .
    container_name: django
    command: python manage.py runserver 0.0.0.0:8000
    volumes:
      - .:/usr/src/app
    ports:
      - "8000:8000"
    depends_on:
      - pgdb

  pgdb:
    image: postgres
    environment:
      - POSTGRES_DB=postgres
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
    container_name: pgdb
    # Все наши знчения будут хранится на удаленой машине
    volumes:
      - pgdbdata:/var/lib/postgresql/data

volumes:
  pgdbdata: null
    
![image](https://github.com/kirillio2/tutorialsWorks/assets/65582386/4c8e7d4e-0911-44b8-9375-99283c6dfce6)

docker-compose run django django-admin startproject nameproject .

docker-compose up

Далее используем уже django команды, таким путем: 
docker-compose run django python manage.py migrate
docker-compose run django python manage.py createsuperuser

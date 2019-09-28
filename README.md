# django_production
This is a Django production-able env with:
```
DB: Postgres
WSGI: Gunicorn
Server: Nginx
```
Other:
```
Django REST
```

## Getting start
### Prerequisites
* docker
* docker-compose

### Dev
Start the server
```
docker-compose up -d --build 
```
### Production
Add these to .env, and modify these fields
* SECRET_KEY
* SQL_DATABASE
* SQL_USER
* SQL_PASSWORD
```
DEBUG=0 
SECRET_KEY=KEY
SQL_ENGINE=django.db.backends.postgresql
SQL_DATABASE=DB_NAME
SQL_USER=DB_USER
SQL_PASSWORD=PASSWORD
SQL_HOST=db
SQL_PORT=5432
DATABASE=postgres
```
Add these to .env.db, and modify these fields
* SQL_DATABASE
* SQL_USER
* SQL_PASSWORD
```
POSTGRES_USER=DB_USER
POSTGRES_PASSWORD=PASSWORD
POSTGRES_DB=DB_NAME
```
Start the server 
```
docker-compose -f docker-compose.prod.yml up -d --build 
docker-compose -f docker-compose.prod.yml exec web python manage.py migrate --noinput
docker-compose -f docker-compose.prod.yml exec web python manage.py collectstatic --no-input --clear
```

## Reference
https://testdriven.io/blog/dockerizing-django-with-postgres-gunicorn-and-nginx/
https://www.django-rest-framework.org/#requirements
https://github.com/twtrubiks/django-rest-framework-tutorial

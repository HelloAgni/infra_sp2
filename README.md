# Infra_sp2
**Проект Infra_sp2 реализует API для сбора отзывов пользователей на произведения.**

***Для работы с проектом необходимо выполнить действия, описанные ниже.***

- git clone <project>
- cd infra_sp2/infra/

**Docker**
- docker-compose up -d
- docker-compose exec web python manage.py migrate
- docker-compose exec web python manage.py collectstatic  
yes
- docker-compose exec web python manage.py import_data  
Y
- docker-compose exec web python manage.py createsuperuser  
...  
Superuser created successfully.  
http://localhost/admin

>>>**Для получения документации по API необходимо открыть в браузере адрес http://localhost/redoc/.**

**POSTMAN**  
Перед началом использования API необходимо выполнить регистрацию пользователя и получить токен  
***Регистрация пользователя***
```sh
POST  http://localhost/api/v1/auth/signup/
{
    "email": "tester1@mail.ru",
    "username": "tester1"
}
Response status 200 OK
{
    "username": "tester1",
    "email": "tester1@mail.ru"
}
```

**Docker**
- docker-compose exec web ls sent_emails  
Copy your file.log <20220603-081115-140473090362512.log>
- docker-compose exec web cat sent_emails/20220603-081115-140473090362512.log  
Код подтверждения: 61b-18466437bce...

**POSTMAN**  
***Получение токена***
```sh
POST  http://localhost/api/v1/auth/token/
{
    "username": "tester1",
    "confirmation_code": "61b-18466437bce..."
}
Response status 200 OK
{
    "token": "eyJ0e..........."
}

Authorization -> Type 'Bearer Token' -> Token -> eyJ0e.........

GET  http://localhost/api/v1/titles
```
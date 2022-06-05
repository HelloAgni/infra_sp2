# Infra_sp2
**Проект Infra_sp2 реализует API для сбора отзывов пользователей на произведения.**

---
***Для работы с проектом необходимо выполнить действия, описанные ниже.***
```bash
git clone <project>
cd infra_sp2/infra/
```
**Docker**
```bash
docker-compose up -d
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py collectstatic
yes
docker-compose exec web python manage.py import_data  
Y
docker-compose exec web python manage.py createsuperuser
...  
> Superuser created successfully.
```
**http://localhost/admin**

>**Для получения документации по API необходимо открыть в браузере адрес http://localhost/redoc/.**

**POSTMAN**  
Перед началом использования API необходимо выполнить регистрацию пользователя и получить токен

***Регистрация пользователя***  
POST  http://localhost/api/v1/auth/signup/
```json
{
    "email": "tester1@mail.ru",
    "username": "tester1"
}
```
```diff
+ Response status 200 OK
```
```json
{
    "username": "tester1",
    "email": "tester1@mail.ru"
}
```

**Docker**
```bash
docker-compose exec web ls sent_emails  
> Copy your file.log <20220603-081115-140473090362512.log>
docker-compose exec web cat sent_emails/<PASTE your file log>
> Код подтверждения: 61b-18466437bce...
```
**POSTMAN**  
***Получение токена***

POST  http://localhost/api/v1/auth/token/
```json
{
    "username": "tester1",
    "confirmation_code": "61b-18466437bce..."
}
```
![#c5f015](https://via.placeholder.com/15/00FF00/000000?text=+) Response status 200 OK
```json
{
    "token": "eyJ0e..........."
}
```
Authorization -> Type 'Bearer Token' -> Token -> eyJ0e.........

GET http://localhost/api/v1/titles  
GET http://localhost/api/v1/titles/1  
GET http://localhost/api/v1/titles/1/reviews  
GET http://localhost/api/v1/titles/5/reviews/6/comments  
GET http://localhost/api/v1/titles/?year=1994  
GET http://localhost/api/v1/titles/?genre=comedy
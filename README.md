# backendCRM

Бэкенд интернет-магазина на Laravel: REST API для клиентов (каталог, покупка, заказы) и админ-панель для управления товарами, категориями и заказами. Оплата реализована через эмулятор платёжной системы с webhook-уведомлениями.

## Возможности

**Клиентский API**
- Регистрация и авторизация по токенам (Laravel Sanctum)
- Каталог: категории, товары по категории, карточка товара
- Покупка товара и список своих заказов (только для авторизованных)
- Создание платежа и приём webhook об оплате

**Админ-панель** (`/admin`)
- Вход по логину/паролю
- CRUD категорий и товаров
- Просмотр заказов
- Страница оплаты-эмулятор (`/pay/{payment}`)

## Стек

PHP · Laravel · Sanctum · MySQL · Blade

## Установка

```bash
git clone https://github.com/d1noy/backendCRM.git
cd backendCRM
composer install
cp .env.example .env
php artisan key:generate
# укажите доступ к БД в .env
php artisan migrate --seed
php artisan serve
```

## API

| Метод | Путь | Доступ | Описание |
|---|---|---|---|
| POST | /api/registration | все | Регистрация |
| POST | /api/auth | все | Вход, выдача токена |
| GET | /api/categories | все | Список категорий |
| GET | /api/categories/{id}/products | все | Товары категории |
| GET | /api/products/{id} | все | Карточка товара |
| POST | /api/products/{id}/buy | токен | Купить товар |
| GET | /api/orders | токен | Мои заказы |
| POST | /api/payments | все | Создать платёж (эмулятор) |
| POST | /api/payment-webhook | платёжка | Уведомление об оплате |

Для защищённых запросов: заголовок `Authorization: Bearer {token}`.

## Схема БД

`users` · `categories` · `products` · `orders` · `payments` · `personal_access_tokens`

## Статус

[Готов]. Планы: [тесты, документация API (Swagger), Docker].

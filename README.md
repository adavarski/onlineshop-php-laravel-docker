### Online Store Class Diagram:
<img src="https://github.com/adavarski/onlineshop-php-laravel-docker/blob/main/pictures/onlinestore-class-diagram.png" width="900">

### Online Store Software Architecture:
<img src="https://github.com/adavarski/onlineshop-php-laravel-docker/blob/main/pictures/onlinestore-software-architecture.png" width="900">

### Online Store Laravel Web session:

<img src="https://github.com/adavarski/onlineshop-php-laravel-docker/blob/main/pictures/laravel-web-session.png" width="900">


### Docker/PHP:Laravel/nginx/mysql example: local development:
``` 
$ docker-compose up -d
Status: Downloaded newer image for nginx:alpine
Creating onlinestore-nginx ... done
Creating onlinestore-app   ... done
Creating onlinestore-db    ... done
$ docker ps -a
CONTAINER ID        IMAGE                   COMMAND                  CREATED             STATUS              PORTS                  NAMES
e73936fcf7f7        nginx:alpine            "/docker-entrypoint.…"   38 seconds ago      Up 37 seconds       0.0.0.0:8000->80/tcp   onlinestore-nginx
43a7bd6b8d38        mysql:5.7               "docker-entrypoint.s…"   38 seconds ago      Up 37 seconds       3306/tcp, 33060/tcp    onlinestore-db
f9b755fb8bae        onlinestore             "docker-php-entrypoi…"   38 seconds ago      Up 34 seconds       9000/tcp               onlinestore-app

$ docker exec -it onlinestore-app rm -rf composer.lock
$ docker exec -it onlinestore-app composer install
$ docker exec -it onlinestore-app php artisan migrate

   INFO  Preparing database.  

  Creating migration table ............................................................................................................... 73ms DONE

   INFO  Running migrations.  

  2014_10_12_000000_create_users_table ................................................................................................... 80ms DONE
  2014_10_12_100000_create_password_resets_table ......................................................................................... 83ms DONE
  2019_08_19_000000_create_failed_jobs_table ............................................................................................ 107ms DONE
  2019_12_14_000001_create_personal_access_tokens_table ................................................................................. 120ms DONE
  2022_02_11_153916_create_products_table ................................................................................................ 61ms DONE
  2022_02_12_140820_alter_users_table .................................................................................................... 85ms DONE
  2022_02_12_152713_create_orders_table ................................................................................................. 143ms DONE
  2022_02_12_152850_create_items_table .................................................................................................. 320ms DONE


$ docker exec -it onlinestore-app php artisan storage:link

   INFO  The [public/storage] link has been connected to [storage/app/public].  

$ docker exec -it onlinestore-app  php artisan key:generate --show
base64:npKVx76GVYs1lNxonOdGYGMp/B5G6JpmiGB3QxuttZc=

$ grep base .env
APP_KEY=base64:npKVx76GVYs1lNxonOdGYGMp/B5G6JpmiGB3QxuttZc=

### Admin add:user
$ docker exec -it onlinestore-app php artisan tinker
Psy Shell v0.11.8 (PHP 8.1.11 — cli) by Justin Hileman
>>> $user = new App\Models\User();
=> App\Models\User {#3705}

>>> $user->setName('davar')
=> null

>>> $user->setEmail('rman@gmail.com');
=> null

>>> $user->setPassword(bcrypt('qwerty123'));
=> null

>>> $user->setBalance(5000);
=> null

>>> $user->setRole('admin');
=> null

>>> $user->save();
=> true

>>> exit
Exit:  Goodbye

Add product: http://localhost:8000/admin/products -> TV product

Register user (new user): ---> Product ->  Add to Chart- -> Purchase -> My Orders

Clean: $ docker-compose down
```

## About Laravel

Laravel is a web application framework with expressive, elegant syntax. We believe development must be an enjoyable and creative experience to be truly fulfilling. Laravel takes the pain out of development by easing common tasks used in many web projects, such as:

- [Simple, fast routing engine](https://laravel.com/docs/routing).
- [Powerful dependency injection container](https://laravel.com/docs/container).
- Multiple back-ends for [session](https://laravel.com/docs/session) and [cache](https://laravel.com/docs/cache) storage.
- Expressive, intuitive [database ORM](https://laravel.com/docs/eloquent).
- Database agnostic [schema migrations](https://laravel.com/docs/migrations).
- [Robust background job processing](https://laravel.com/docs/queues).
- [Real-time event broadcasting](https://laravel.com/docs/broadcasting).

Laravel is accessible, powerful, and provides tools required for large, robust applications.


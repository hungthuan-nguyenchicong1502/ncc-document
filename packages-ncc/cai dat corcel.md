## run .env

```
@cd $(LARAVEL_APP_PATH) && \
        php artisan key:generate && \
		php artisan migrate && \
		php artisan optimize:clear
```
## install corcel
```
cd $(LARAVEL_APP_PATH) && \
		composer require jgrossi/corcel && \
		php artisan vendor:publish --provider="Corcel\Laravel\CorcelServiceProvider"
```
## /laravel-app/config/database.php

```
'corcel' => [
            'driver' => 'mariadb',
            'url' => env('DB_URL'),
            'host' => env('DB_HOST', '127.0.0.1'),
            'port' => env('DB_PORT', '3306'),
            'database' => env('DB_DATABASE', 'laravel'),
            'username' => env('DB_USERNAME', 'root'),
            'password' => env('DB_PASSWORD', ''),
            'unix_socket' => env('DB_SOCKET', ''),
            'charset' => env('DB_CHARSET', 'utf8mb4'),
            'collation' => env('DB_COLLATION', 'utf8mb4_unicode_ci'),
            'prefix' => 'wp_',
            'prefix_indexes' => true,
            'strict' => true,
            'engine' => null,
            'options' => extension_loaded('pdo_mysql') ? array_filter([
                (PHP_VERSION_ID >= 80500 ? Mysql::ATTR_SSL_CA : PDO::MYSQL_ATTR_SSL_CA) => env('MYSQL_ATTR_SSL_CA'),
            ]) : [],
        ],
```

## test tinker
```
cd $(LARAVEL_APP_PATH) && \
		echo "Corcel\Model\Post::first();" | php artisan tinker
```
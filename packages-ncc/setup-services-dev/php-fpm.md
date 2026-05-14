```
define WP_APP_PROXY_FIX_CODE
if (isset($$_SERVER['HTTP_X_FORWARDED_PROTO']) && $$_SERVER['HTTP_X_FORWARDED_PROTO'] === 'https') {
    $$_SERVER['HTTPS'] = 'on';
}
endef
```
## comoposer setup
```
composer global require wp-cli/wp-cli-bundle
	ln -s ~/.composer/vendor/bin/wp /usr/sbin/wp || true
	wp --version

@if [ ! -f $(WP_APP_PATH)/wp-settings.php ]; then \
		wp core download --path=$(WP_APP_PATH); \
	fi
# 	note apk add --no-cache php84-mysqli mariadb-client
	@if [ ! -f $(WP_APP_PATH)/wp-config.php ]; then \
		printf "$$WP_APP_PROXY_FIX_CODE" > /tmp/proxy_fix.php; \
		wp config create \
			--dbname=$(DB_DATABASE) \
			--dbuser=$(DB_USERNAME) \
			--dbpass=$(DB_PASSWORD) \
			--dbhost=$(DB_HOST) \
			--dbcharset=$(DB_CHARSET) \
			--dbcollate=$(DB_COLLATE) \
			--path=$(WP_APP_PATH) \
			--extra-php < /tmp/proxy_fix.php \
			--allow-root; \
		rm -f /tmp/proxy_fix.php; \
	fi
	wp db check --path=$(WP_APP_PATH)

	if ! wp core is-installed --path=$(WP_APP_PATH) --allow-root; then \
		wp core install --path=/$$WP_PATH \
				--url=$(WP_URL) \
				--title=$(WP_TITLE) \
				--admin_user=$(WP_ADMIN) \
				--admin_password=$(WP_ADMIN_PASSWORD) \
				--admin_email=$(WP_ADMIN_EMAIL) \
				--skip-email \
				--allow-root; \
	fi

	if [ -f $(WP_APP_PATH)/wp-config.php ]; then \
			wp config set WP_HOME $(WP_URL) --path=$(WP_APP_PATH) --allow-root; \
			wp config set WP_SITEURL $(WP_URL) --path=$(WP_APP_PATH) --allow-root; \
			wp config set WP_POST_REVISIONS 1 --raw --path=$(WP_APP_PATH) --allow-root; \
			wp option update thumbnail_size_w 400 --autoload=yes --path=$(WP_APP_PATH) --allow-root || true; \
			wp option update thumbnail_size_h 400 --autoload=yes --path=$(WP_APP_PATH) --allow-root || true; \
			wp option update medium_size_w 0 --autoload=no --path=$(WP_APP_PATH) --allow-root || true; \
			wp option update medium_size_h 0 --autoload=no --path=$(WP_APP_PATH) --allow-root || true; \
			wp option update large_size_w 0 --autoload=no --path=$(WP_APP_PATH) --allow-root || true; \
			wp option update large_size_h 0 --autoload=no --path=$(WP_APP_PATH) --allow-root || true; \
			wp option update medium_large_size_w 0 --autoload=no --path=$(WP_APP_PATH) --allow-root || true; \
			wp option update medium_large_size_h 0 --autoload=no --path=$(WP_APP_PATH) --allow-root || true; \
	fi

```
chown -R nobody:root /laravel-app/wp-app

chmod -R 775 /laravel-app/wp-app

ln -s /laravel-app/wp-app/wp-content/uploads /laravel-app/public/uploads

# fix debug
php -m | grep mysqli

pgrep -o php-fpm

kill 20313

kill -USR2 $(pgrep -o php-fpm)

php-fpm -D

ps aux | grep php-fpm

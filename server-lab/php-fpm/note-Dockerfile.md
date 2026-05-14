# cap quang
RUN sed -i 's/dl-cdn.alpinelinux.org/mirror.leaseweb.com/g' /etc/apk/repositories

## run wp
```
RUN apk add --no-cache \
	php84-fpm \
	php84-mysqli \
	php84-gd
```
# run nginx
RUN sed -i 's/listen = 127.0.0.1:9000/listen = 0.0.0.0:9000/' /etc/php84/php-fpm.d/www.conf

# docker logs
RUN ln -sf /dev/stdout /var/log/php84/error.log

# run project - user nobody
```
RUN chown -R nobody:nobody /var/www/html /var/log/php84 && \
    chmod -R 775 /var/www/html /var/log/php84
```
USER nobody

CMD ["php-fpm84", "-F"]
# run project - user root
```
RUN chown -R root:nobody /var/www/html /var/log/php84 && \
    chmod -R 775 /var/www/html /var/log/php84
```
CMD ["php-fpm84", "-F"]

CMD ["php-fpm84", "-F", "-R"]

## ext laravel
```
RUN apk add --no-cache \
    php84-tokenizer \
    php84-session \
    php84-dom \
    php84-xml \
    php84-xmlwriter \
    php84-fileinfo \
    php84-pdo \
    php84-pdo_sqlite \
    php84-pdo_mysql
```
CMD ["sh", "-c", "tail -f >/dev/nul"]
## ext imp
```
apk add --no-cache php84 \
    php84-fpm \
    php84-ctype \
    php84-curl \
    php84-dom \
    php84-fileinfo \
    php84-gd \
    php84-gettext \
    php84-iconv \
    php84-intl \
    php84-mbstring \
    php84-openssl \
    php84-pdo \
    php84-pdo_mysql \
    php84-pdo_sqlite \
    php84-phar \
    php84-session \
    php84-tokenizer \
    php84-xml \
    php84-xmlreader \
    php84-xmlwriter \
    php84-zip \
    php84-zlib \
    php84-bcmath \
    php84-sodium \
    php84-opcache
```
# default
.DEFAULT_GOAL :=help

RUN printf "https://mirror.leaseweb.com/alpine/latest-stable/main\\nhttps://mirror.leaseweb.com/alpine/latest-stable/community\\n" \\
	> /etc/apk/repositories

PHP_FPM_NAME_APP_ENV := $(PHP_FPM_NAME)

ifeq ($(APP_ENV), dev)
	PHP_FPM_NAME_APP_ENV := $(PHP_FPM_NAME)-dev
endif

docker restart $(PHP_FPM_NAME_APP_ENV)

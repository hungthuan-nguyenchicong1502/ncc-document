# default
```
define PHP_FPM_DOCKER_COMPOSE_YML
services:
 $(PHP_FPM_NAME):
  build:
   context: .
   dockerfile: Dockerfile
  
  image: $(PHP_FPM_NAME)
  container_name: $(PHP_FPM_NAME)

  restart: always

  networks:
   - $(PHP_FPM_NAME)-net

  volumes:
   - $(VOLUMES_PROJECT_APP):/var/www/html

networks:
 $(PHP_FPM_NAME)-net:
  external: true
  name: $(MY_APP_NET)
endef
```
## run
```
LARAVEL_COMPOSE_FILES := -f $(LARAVEL_PROJECT_PATH)/docker-compose.yml

ifeq ($(APP_ENV), dev)
	LARAVEL_COMPOSE_FILES := -f $(LARAVEL_PROJECT_PATH)/docker-compose.dev.yml
endif

# compose
@echo "_laravel/_docker-compose.mk-build"
	docker compose $(LARAVEL_COMPOSE_FILES) \
		--project-directory $(LARAVEL_PROJECT_PATH) \
		up -d --build

@echo "_laravel/_docker-compose.mk-up"
	docker compose $(LARAVEL_COMPOSE_FILES) \
		--project-directory $(LARAVEL_PROJECT_PATH) \
		up -d

@echo "_laravel/_docker-compose.mk-down"
	docker compose $(LARAVEL_COMPOSE_FILES) \
		down
```
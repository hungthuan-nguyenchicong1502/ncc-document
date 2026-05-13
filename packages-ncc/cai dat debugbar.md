## # composer require fruitcake/laravel-debugbar --dev

```
	cd $(LARAVEL_APP_PATH) && \
		composer require fruitcake/laravel-debugbar --dev

test-debugbar:
	{{debug($data)}}
```
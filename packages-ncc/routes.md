# routes.php
```
Route::get('/', function() {
    return view('ncc-views::index');
})->name('index');

Route::get('/category/{slug}', [NCC\Wp\Categories\CategoryController::class, 'show'])->name('category');
```
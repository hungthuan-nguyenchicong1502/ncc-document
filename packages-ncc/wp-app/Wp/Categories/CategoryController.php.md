# Wp/Categories/CategoryController.php
```
<?php

namespace NCC\Wp\Categories;

use App\Http\Controllers\Controller;

class CategoryController extends Controller
{
    // http://127.0.0.1:8000/category/uncategorized
    public function show(string $slug, CategoryServices $services) {
        $data = $services->services($slug);
        return view('ncc-views::category', ['data' => $data]);
    }
}
```
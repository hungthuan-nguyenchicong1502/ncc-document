# Wp/Categories/CategoryLoader.php
```
<?php

namespace NCC\Wp\Categories;

use Corcel\Model\Taxonomy;

class CategoryLoader extends Taxonomy
{
    // app(NCC\Wp\Categories\CategoryLoader::class)->loader('uncategorized')
    public function loader(string $slug)
    {
        return $this->getCategory($slug);
    }

    public function getCategory(string $slug)
    {
        // $category = self::first();
        $category = self::slug($slug)
            ->firstOrFail();
        return $category;
    }
}
```
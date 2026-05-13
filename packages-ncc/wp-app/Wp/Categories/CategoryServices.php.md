# Wp/Categories/CategoryServices.php

```
<?php

namespace NCC\Wp\Categories;

class CategoryServices
{
    public function __construct(
        protected CategoryLoader $loader
    ){}

    // app(NCC\Wp\Categories\CategoryServices::class)->services('uncategorized')
    public function services(string $slug)
    {
        return $this->getLoader($slug);
    }

    public function getLoader(string $slug)
    {
        $data = $this->loader->loader($slug);
        return $data;
    }
}
```
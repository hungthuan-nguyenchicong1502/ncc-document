# NCCServiceprovider.php

```
<?php

namespace NCC;

use Illuminate\Support\ServiceProvider;

class NCCServiceprovider extends ServiceProvider
{
    public function boot()
    {
        $this->loadRoutesFrom(__DIR__ . '/routes.php');
        $this->loadViewsFrom(__DIR__ . '/views', 'ncc-views');
    }
}
```
## run
php artisan route:list
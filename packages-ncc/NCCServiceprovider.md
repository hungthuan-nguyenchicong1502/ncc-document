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
    }
}
```
## run
php artisan route:list
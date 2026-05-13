# NCCAggregateServiceProvider
```
<?php

namespace NCC;

use Illuminate\Support\AggregateServiceProvider;

class NCCAggregateServiceProvider extends AggregateServiceProvider
{
    protected $providers = [
        NCCServiceprovider::class
    ];
}
```
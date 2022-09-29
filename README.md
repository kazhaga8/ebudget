# ebudget

## New File

```php
// routes/api_ebudget.php
<?php

use Illuminate\Http\Request;
use Illuminate\Support\Facades\Route;

/*
|--------------------------------------------------------------------------
| API Routes
|--------------------------------------------------------------------------
|
| Here is where you can register API routes for your application. These
| routes are loaded by the RouteServiceProvider within a group which
| is assigned the "api" middleware group. Enjoy building your API!
|
*/
Route::get('/connectionTest', 'ApiController@connectionTest')->name('connectionTest');

```
```php
// app/Http/Controllers/Api/EBudget/ApiController.php
<?php


namespace App\Http\Controllers\Api\EBudget;

use Illuminate\Support\Facades\DB;

use App\Http\Controllers\Controller;


class ApiController extends Controller
{
    public function connectionTest()
    {
        $actual = DB::connection('ebudget')->table('REPORT')->first();
        return response()->json($actual);
    }
}

```

## Edit File
````php
// config/database.php
  <?php

    'connections' => [
```

        'ebudget' => [
            'driver' => 'sqlsrv',
            'url' => env('DATABASE_URL'),
            'host' => env('DB_EBUDGET_HOST', 'localhost'),
            'port' => env('DB_EBUDGET_PORT', '1433'),
            'database' => env('DB_EBUDGET_DATABASE', 'forge'),
            'username' => env('DB_EBUDGET_USERNAME', 'forge'),
            'password' => env('DB_EBUDGET_PASSWORD', ''),
            'charset' => 'utf8',
            'prefix' => '',
            'prefix_indexes' => true,
        ],

```
    ],

];

````
````php
// app/Providers/RouteServiceProvider.php
<?php

    protected function mapApiRoutes()
    {
    
    ```    
        Route::prefix('api/ebudget')
            ->middleware('api')
            ->namespace("{$this->apiNamespace}\EBudget")
            ->group(base_path('routes/api_ebudget.php'));
    ```
    }
}

````
````.env
```
DB_CONNECTION=ebudget
DB_EBUDGET_PORT=3306
DB_EBUDGET_HOST=127.0.0.1
DB_EBUDGET_DATABASE=ebadget
DB_EBUDGET_USERNAME=root
DB_EBUDGET_PASSWORD=root
```
````

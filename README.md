# laravel-restful-api
Building RESTful APIs in Laravel

## Create laravel 9 project
```
composer create-project laravel/laravel laravel-restful-api
```

## Create Petition model
1. m for migration file
2. f for factory
3. s for seeder
```
php artisan make:model Petition -mfs
```

## Now open Petition migration file
```
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('petitions', function (Blueprint $table) {
            $table->id();
            $table->string('title');
            $table->text('category');
            $table->text('description');
            $table->string('author');
            $table->integer('signees');
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('petitions');
    }
};

```

## Create Author model
1. m for migration file
2. f for factory
3. s for seeder
```
php artisan make:model Author -mfs
```

## Now open Author migration file
```
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('authors', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('authors');
    }
};

```
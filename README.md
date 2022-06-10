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

## Migrate project

```
php artisan migrate
```
Note: Make sure your database connection is ok, please change database in .env file

## Now open Petition model and changed

```
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Petition extends Model
{
    use HasFactory;

    protected $fillable = ['title', 'description', 'category', 'author', 'signees'];
}

```

## Now open Author model and changed

```
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Author extends Model
{
    use HasFactory;

    protected $fillable = ['name'];
}
```

## Create DB Seed
Goto database/factories/PetitionFactory.php

```
<?php

namespace Database\Factories;

use Illuminate\Database\Eloquent\Factories\Factory;

/**
 * @extends \Illuminate\Database\Eloquent\Factories\Factory<\App\Models\Petition>
 */
class PetitionFactory extends Factory
{
    /**
     * Define the model's default state.
     *
     * @return array<string, mixed>
     */
    public function definition()
    {
        return [
            'title' => $this->faker->word,
            'category' => $this->faker->text(50),
            'description' => $this->faker->text(200),
            'author' => $this->faker->name,
            'signees' => $this->faker->numberBetween(0, 100000)
        ];
    }
}

```

Goto database/factories/AuthorFactory.php

```
<?php

namespace Database\Factories;

use Illuminate\Database\Eloquent\Factories\Factory;

/**
 * @extends \Illuminate\Database\Eloquent\Factories\Factory<\App\Models\Author>
 */
class AuthorFactory extends Factory
{
    /**
     * Define the model's default state.
     *
     * @return array<string, mixed>
     */
    public function definition()
    {
        return [
            'name' => $this->faker->name
        ];
    }
}

```

## Now define both factory files in seeders file

Goto database/seeders/PetitionSeeder.php

```
<?php

namespace Database\Seeders;

use Illuminate\Database\Console\Seeds\WithoutModelEvents;
use Illuminate\Database\Seeder;

class PetitionSeeder extends Seeder
{
    /**
     * Run the database seeds.
     *
     * @return void
     */
    public function run()
    {
        \App\Models\Petition::factory()->times(50)->create();
    }
}

```

Goto database/seeders/AuthSeeder.php

```
<?php

namespace Database\Seeders;

use Illuminate\Database\Console\Seeds\WithoutModelEvents;
use Illuminate\Database\Seeder;

class AuthorSeeder extends Seeder
{
    /**
     * Run the database seeds.
     *
     * @return void
     */
    public function run()
    {
        \App\Models\Author::factory()->times(10)->create();
    }
}

```

## Run db:seed

```
php artisan db:seed --class=PetitionSeeder
php artisan db:seed --class=AuthorSeeder
```

## Create PetitionController, PetitionResource, PetitionCollection

```
php artisan make:controller PetitionController --api --model=Petition
php artisan make:resource PetitionResource
php artisan make:resource PetitionCollection
```

## Create AuthorController, AuthorResource, AuthorCollection

```
php artisan make:controller PetitionController --api --model=Petition
php artisan make:resource PetitionResource
php artisan make:resource PetitionCollection
```
# Fundamental plan to get information
1. Learn migrations & models
2. Learn controllers
3. Learn views
4. Complete the MVC model
# First step.
I need to create 3 migrations.
1. First migration should create a genres table with ID, genre's name fields
2. Second migration should create a movies table with ID, movie's name, publication status(is published: true/false), link to poster(image)
3. Third migration should create a table which links previous two tables

## Information
Migration can be created by using artisan util
For example:
```sh
php artisan make:migration create_flights_table
```

### Migration structure

A migration class contains two methods: `up` and `down`. The `up` method is used to add new tables, columns, or indexes to your database, while the `down` method should reverse the operations performed by the `up` method.

Example of migration:
```php
<?php
 
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;
 
return new class extends Migration
{
    /**
     * Run the migrations.
     */
    public function up(): void
    {
        Schema::create('flights', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('airline');
            $table->timestamps();
        });
    }
 
    /**
     * Reverse the migrations.
     */
    public function down(): void
    {
        Schema::drop('flights');
    }
};
```

To migrate(all unapplied migrations) execute the command:
```sh
php artisan migrate
```

### Detailed review of migration structure

1. Creating a new tables is a function of the `Schema::create` method. 
2. The create method accepts two arguments: the first is the name of the table, while the second is a closure which receives a Blueprint object that may be used to define the new table.
Example: 
```php
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;
 
Schema::create('users', function (Blueprint $table) {
    $table->id();
    $table->string('name');
    $table->string('email');
    $table->timestamps();
});
```
3. You may determine the existence of a table or column using the hasTable and hasColumn methods. Example:
```php
if (Schema::hasTable('users')) {
    // The "users" table exists...
}
 
if (Schema::hasColumn('users', 'email')) {
    // The "users" table exists and has an "email" column...
}
```

4. Check here all available data types for table columns/fields: 
https://laravel.com/docs/10.x/migrations#available-column-types

Most common types in usage are: 
```php
$table->id(); // auto increment id for every row
$table->string('field_name'); // string value
$table->timestamps(); // timestamp (when row was created)
$table->foreignId('any foreign field name'); // foreign id for foreign row
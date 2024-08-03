# PHP and Laravel Cheat Sheet

## PHP Cheat Sheet

### Basic Syntax

```php
<?php
// Single-line comment

/*
 * Multi-line comment
 */

// Variables
$name = "John";
$age = 25;

// Constants
define('PI', 3.14);

// Arrays
$colors = array('red', 'green', 'blue'); // old syntax
$colors = ['red', 'green', 'blue']; // shorthand

// Associative Arrays
$user = [
    "name" => "John",
    "age" => 25
];

// Functions
function greet($name) {
    return "Hello, " . $name;
}

echo greet($name); // Output: Hello, John
?>
```

### Arrays
```php
// Indexed Array
$fruits = ["apple", "banana", "cherry"];

// Associative Array
$person = [
    "first_name" => "John",
    "last_name" => "Doe"
];

// Multi-dimensional Array
$contacts = [
    ["name" => "John", "phone" => "123-456-7890"],
    ["name" => "Jane", "phone" => "987-654-3210"]
];

// Array Functions
$count = count($fruits);
$keys = array_keys($person);
$values = array_values($person);
```

### Strings
```php
// Concatenation
$full_name = $first_name . " " . $last_name;

// String Functions
$length = strlen($full_name);
$uppercase = strtoupper($full_name);
$lowercase = strtolower($full_name);
$replaced = str_replace("John", "Jane", $full_name);
```

### Working with Files
```php
// Reading a file
$content = file_get_contents('file.txt');

// Writing to a file
file_put_contents('file.txt', 'Hello, World!');
```


## Laravel Cheat Sheet
### Artisan Commands
```bash
# Create a new Laravel project
composer create-project --prefer-dist laravel/laravel myProject

# Start the development server
php artisan serve

# Create a new controller
php artisan make:controller MyController

# Create a new model
php artisan make:model MyModel

# Create a new migration
php artisan make:migration create_users_table

# Run migrations
php artisan migrate

# Rollback migrations
php artisan migrate:rollback

# Generate a new key
php artisan key:generate
```

### Routing
``` php
// Basic Route
Route::get('/', function () {
    return 'Hello, World!';
});

// Route with Parameters
Route::get('/user/{id}', function ($id) {
    return 'User ID: ' . $id;
});

// Named Route
Route::get('/profile', function () {
    return view('profile');
})->name('profile');

// Route with Controller
Route::get('/user/{id}', [UserController::class, 'show']);
```

### Controllers
```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class UserController extends Controller
{
    public function index()
    {
        return view('user.index');
    }

    public function show($id)
    {
        return view('user.show', ['id' => $id]);
    }
}

````

### Views
```blade
<!-- resources/views/user/index.blade.php -->
<!DOCTYPE html>
<html>
<head>
    <title>User Index</title>
</head>
<body>
    <h1>User Index</h1>
</body>
</html>

<!-- resources/views/user/show.blade.php -->
<!DOCTYPE html>
<html>
<head>
    <title>User Show</title>
</head>
<body>
    <h1>User ID: {{ $id }}</h1>
</body>
</html>
```

### Eloquent ORM
```php
// Model
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    protected $fillable = ['name', 'email'];
}

// Retrieving Data
$users = User::all();
$user = User::find(1);
$user = User::where('email', 'example@example.com')->first();

// Inserting Data
User::create(['name' => 'John', 'email' => 'john@example.com']);

// Updating Data
$user->update(['name' => 'Jane']);

// Deleting Data
$user->delete();
Migrations
php
Copy code
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreateUsersTable extends Migration
{
    public function up()
    {
        Schema::create('users', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('email')->unique();
            $table->timestamps();
        });
    }

    public function down()
    {
        Schema::dropIfExists('users');
    }
}
```

### Validation
```php
use Illuminate\Support\Facades\Validator;

// Basic Validation
$request->validate([
    'name' => 'required|max:255',
    'email' => 'required|email'
]);

// Custom Validation Messages
$validator = Validator::make($request->all(), [
    'name' => 'required|max:255',
    'email' => 'required|email'
], [
    'name.required' => 'The name field is required.'
]);

if ($validator->fails()) {
    return redirect()->back()->withErrors($validator)->withInput();
}
```

### Authentication
```php
// User Authentication
use Illuminate\Support\Facades\Auth;

// Login
if (Auth::attempt(['email' => $email, 'password' => $password])) {
    // Authentication passed
    return redirect()->intended('dashboard');
}

// Logout
Auth::logout();
return redirect('/');

// Middleware for Auth
Route::get('/dashboard', function () {
    // Only authenticated users may enter...
})->middleware('auth');

```

### Middleware
```php
Copy code
<?php

namespace App\Http\Middleware;

use Closure;
use Illuminate\Support\Facades\Auth;

class CheckAge
{
    public function handle($request, Closure $next)
    {
        if (Auth::user() && Auth::user()->age < 18) {
            return redirect('home');
        }

        return $next($request);
    }
}
```

### Tinker
```bash
# Open Tinker (REPL)
php artisan tinker

# Example Commands in Tinker
$user = App\Models\User::find(1);
$user->name = 'John Doe';
$user->save();
Simpan file ini sebagai README.md di repositori GitHub Anda. Cheat sheet ini mencakup dasar-dasar PHP dan Laravel yang sering digunakan, termasuk sintaks umum, perintah Artisan, routing, controllers, views, Eloquent ORM, migrations, validation, authentication, middleware, dan Tinker.
```

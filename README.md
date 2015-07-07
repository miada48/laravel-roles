# Laravel Roles
Laravel 5 User Role Manager

The idea of this package came from laracast [laracasts/Users-and-Roles-in-Laravel](https://github.com/laracasts/Users-and-Roles-in-Laravel) and now it is built for laravel 5.

### Requirements
    Laravel >=5.1
    PHP >= 5.5.9 
    
## Installation

1. Run 
    ```
    composer require "appzcoder/laravel-roles":"dev-master"
    ```
    
2. Add service provider into **/config/app.php** file.
    ```php
    'providers' => [
        ...
    
        Appzcoder\LaravelRoles\LaravelRolesServiceProvider::class,
    ],
    ```
3. Run **composer update**

4. Publish migrations
    ```
    php artisan vendor:publish
    ```

5. Add the bollow lines to your **user model** located at **/app/User.php**
    ```php
    // Put the line bofore the class declaration and after the namespace
    use Appzcoder\LaravelRoles\Traits\RoleTrait;
    
    // Put the line inside of the user class
    use RoleTrait;
    ```
    
[Note: Need to configure database and need to run migrate command **php artisan migrate** ]

## Usage

Use the routes as bellow.

```php
Route::get('/roles', function () {

    /* Create user if needed
    App\User::create([
    'name' => 'Sohel Amin',
    'email' => 'sohelamincse@gmail.com',
    'password' => bcrypt('123456'),
    ]);
     */

    $user = App\User::first();

    /* Create roles
    $role = new Appzcoder\LaravelRoles\Models\Role;
    $role->name = 'admin';
    $role->save();
     */

    /* Assign and remove role from user
    $role = Appzcoder\LaravelRoles\Models\Role::whereName('admin')->first();
    $user->assignRole($role);
    //$user->removeRole(2);
     */

    return $user->roles;
});

Route::get('/admin', ['middleware' => 'role:admin', 'uses' => 'AdminController@index']);
```

##Author

<a href="http://www.sohelamin.com">Sohel Amin</a>

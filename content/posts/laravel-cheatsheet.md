+++
categories = ["laravel", "php"]
date = "2021-04-04"
description = "Laravel Cheatsheet"
title = "Laravel Cheatsheet"
+++

This Laravel cheatsheet is tested on Ubuntu with PHP 7.1 and 7.2 but it should work everywhere.

##  Installation (Ubuntu)
### Install Dependencies
```bash
sudo apt install mysql-server php-xml php-mysql php-bcmath php-mbstring
```
Feel free remove `php-bcmath` if not going to use Telescope

### Install composer and set path

```bash
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === '93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```

Assuming composer is installed in `/home/ravindra/Installation/Composer` then path values should be as follows.

```bash
PATH=$PATH:/home/ravindra/Installation/Composer
PATH=$PATH:$HOME/.config/composer/vendor/bin
```

### Install Laravel installer

```bash
composer global require laravel/installer
```

## Using Model factory

### Generate 20 fake users
```php
$users = factory(App\User::class, 20)->create();
```

### Generate 10 fake users with account_type variable set to admin
```php
$user = factory(App\User::class, 5)->create([
	'account_type' => 'admin'
]);
```

##  Authorization

* Abort if user doesn't own project (In Controller)

```php
public function show(Project $project){
	abort_if ($project->owner_id != auth()->id(), 403);
}
```

* Adding a method to user model (In Controller)

```php
public function show(Project $project){
	abort_if (! auth()->user->owns($project), 403);
}
```

or

```php
public function show(Project $project){
	abort_unless (auth()->user->owns($project), 403);
}
```
---
### Using Policy

* Create a policy for project model  (In Terminal)

```bash
php artisan make:policy -m Project ProjectPolicy
```
or

```
php artisan make:policy ProjectPolicy --model=Project
```

* Register a policy  (In AuthServiceProvider)

Open `app/Providers/AuthServiceProvider.php` and change `$policies` array according to your need

```php
protected $policies = [
	'App\Project' => 'App\Policies\ProjectPolicy',
]
```

* Abort if user doesn't own the project (In Policy)

```php
public function view(User $user, Project $project){
	return project->owner_id == $user->id;
}
```

* Using without project (In Policy)

```php
public function create(User $user){
	return $user->account_type == 'Admin';
}
```

* Using policy with project (In Controller)

```php
public function show(Project $project){
	$this->authorize('view', $project);
}
```

* Using policy without project (In Controller)

```php
public function create(){
	$this->authorize('create', Project::class);
}
```

---
### Using Gate

* Using gate (In Controller)

```php
public function update(Project $project){
	abort_if(\Gate::denies('update', $project), 403);
}
```

or

```php
public function update(Project $project){
	abort_unless(\Gate::allows('update', $project), 403);
}
```

---
### Using Routes

* Using middleware on a resource (In web.php)

```php
Route::resource('project', 'ProjectController')
->middleware('can:update, project');
```

---
### Using Views

* Using blade files (random.blade.php)

```php
@can('update', $project)
	update related stuff
@endcan
```

---
### Admin Override

Open `app/Providers/AuthServiceProvider.php`

\Illuminate\Auth

```php
public function boot(Gate $gate){
	$this->registerPolicies();
	
	$gate->before(function ($user){
		return $user->isAdmin();
	});
}
```



### Setting Laravel Passport
- Install Passport via composer: `composer require laravel/passport`
- Migrate Database: `php artisan migrate`
- Install to generate keys: `php artisan passport:install` and save output somewhere or don't
- Extend User Model by adding HasApiTokens Trait
```php
use Laravel\Passport\HasApiTokens;

class User extends Authenticatable
{
  use HasApiTokens, Notifiable;
}
```
- Register routes in `AuthServiceProvider`
```php
use Laravel\Passport\Passport;
class AuthServiceProvider extends ServiceProvider
{

    public function boot()
    {
        $this->registerPolicies();
        Passport::routes();
    }
}
```

- Config auth driver: `config/auth.php` set driver and guard to passport
```php
	'guards' => [
			'web' => [
					'driver' => 'session',
					'provider' => 'users',
			],

			'api' => [
					'driver' => 'passport', //here
					'provider' => 'users',
			],
	],
```

- Pull Vue Components: `php artisan vendor:publish --tag=passport-components`
- Register components:
```js
Vue.component(
    'passport-clients',
    require('./components/passport/Clients.vue').default
);

Vue.component(
    'passport-authorized-clients',
    require('./components/passport/AuthorizedClients.vue').default
);

Vue.component(
    'passport-personal-access-tokens',
    require('./components/passport/PersonalAccessTokens.vue').default
);
```

# Deploy
- `php artisan passport:keys`
- `php artisan passport:client`

## Echo SQL Query for all pending migrations
```bash
php artisan migrate --pretend
```

### Tinker Tricks
## Truncate a table
```php
	User::truncate();
```


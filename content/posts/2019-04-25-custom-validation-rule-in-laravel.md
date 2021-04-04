+++
categories = ["laravel", "validation"]
date = "2021-04-04"
description = "How to create a custom validation rule in Laravel"
title = "Custom Validation Rule in Laravel"
+++

# Creating Custom Validation Rule

Validation is used by everyone because we can't trust user input, today we are going to create a new validation rule named `AlphaSpace`, it will be used to make sure use input contains alphabets and spaces, we need to create a new validation rule, to do that open terminal and type

```bash
php artisan make:rule AlphaSpace
```

It will create a new file in `App/Rules` named `AlphaSpace`, in that file we have 3 metohds
```php

// Construction
public function __construct()
{
    //
}

// Validation Logic is goes here
public function passes($attribute, $value)
{
    //
}

// Validation error messages goes here
public function message()
{
    return 'The validation error message.';
}
```

Let's add some content to this file to make it valid
```php
public function passes($attribute, $value)
{
    return preg_match('/(^[A-Za-z ]+$)+/', $value);
}

public function message()
{
    return 'The :attribute contains invalid characters.';
    // :attribute refers to attribute name
}
```

# How to Use Custom Validation Rule in Laravel

We can use this validation is FormRequest, Controller or anywhere we need.

Let's do it in FormRequest because that's where we should keep our validation logic.

```php
use App\Rules\AlphaSpace;
// Import it

...
public function rules()
{
	return [
		...
		'name' => ['required', 'string', 'min:2', 'max:64', new AlphaSpace],
		...
	]
}
```

And we are done.
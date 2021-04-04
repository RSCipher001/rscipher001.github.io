+++
categories = ["laravel", "intervention"]
date = "2021-04-04"
description = "How to use resize images in Laravel"
title = "How to Resize Images in Laravel"
+++

# Introduction

Image uploading is a common thing among web applications and in many situations we have to process those images before showing them back to users, we may have to resize images, generate thumbnails, etc. We are going to use Intervention package for that in Laravel, it can work with both `gd` and `imagick` library, I'd suggest you to use imagick. Let's get started

# Steps
- Install Intervention
- Update Configuration
- Save And Resize Image in Controller

# Install Intervention
Go to http://image.intervention.io/ and follow installation instructions, I am also going to put those instruction here but remember following official guides are better anyways open terminal and type

```bash
composer require intervention/image
```

Open `config/app.php` and add the following lines

in the `$providers` array
```php
Intervention\Image\ImageServiceProvider::class,
```

in the `$aliases` array
```php
'Image' => Intervention\Image\Facades\Image::class
```

# Update Configuration
*NOTE 1:* Tools like XAMPP doesn't come with imagick support so if you're a XAMPP user then skip this step.
*NOTE 2:* In most linux systems you've to manually install imagick, in Ubuntu you can type `sudo apt install php-imagick` to install it.

By default Intervention uses GD library and we want to use `imagick` so we will pull configuration files and change our driver from `gd` to `imagick`, open terminal and type
```bash
php artisan vendor:publish --provider="Intervention\Image\ImageServiceProviderLaravel5"
```

Now you can access intervention config in `config/image.php`, just change your driver from `gd` to `imagick` and you're good to go.

# Save And Resize Image in Controller

I assume you've completed first step, we will take a look at file upload example, here is HTML code
```html
<input name="image" type="file" accept="image/jpeg" required>
```

We will have validation in Controller or Form Request like this
```php
// This is a form request code snippet but validation rules are same everywhere
// Laravel also allows us to set dimensions option for images
public function rules()
    {
        return [
            'image' => 'required|image|mimes:jpeg,jpg|dimensions:min_width=1000,ratio=1/1',
        ];
    }
```

Our Controller will look like this.
```php
// This example uses a form request class but you're free to implement controller level validation
public function store(ImageRequest $request)
{
    // Save image and get path
    $path = $request->image->storeAs('images', md5_file($request->image) . '.jpg', 'public');
    // In storeAs method first argument 'images' is folder name, second argument is md5sum for file to avoid redundancy when same file uploaded twice, and this argument public is used when we want to store image in public directory.

    // Generate a thumbnail
    // use Intervention\Image\Facades\Image;
    $realPath = 'storage/' . $path;
    Image::make($realPath)->resize(400, 400)->save($realPath);

    // Make functions take file path as argument, save function stores files to given location, in this case we are updating original file.
}
```
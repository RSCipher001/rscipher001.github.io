+++
categories = ["laravel", "relationships"]
date = "2021-04-04"
description = "How to get started with many to many relationship in Laravel"
title = "Laravel Many to Many Relationship"
+++

# Getting Started

Many to many relationship are awesome but they are little different from other type of relations, it this post we are going to see that how can we create many to many relationships in laravel and I am going to use `attribute` and `product` example because I am working on it. This is part of an e-commerce website where a product can have many attributes like color, size, etc and an attribute can belong to many products. First we will create our models and define relationships in our models.

```bash
php artisan make:model -a Product
php artisan make:model -a Attribute
```

`-a` options creates model, migration, controller and Factory, if you don't need factory then use `-mcr` instead `-a`.


Now let's define relationships in our models

```php
// Product.php
public function attributes()
{
    return $this->belongsToMany('App\Attribute');
}
```

```php
// Attribute.php
public function products()
{
    return $this->belongsToMany('App\Product');
}
```

Feel free to add some columns to your migration files, I am going to skip that because we don't need that. Since this is a m-2-m relationship we need an intermediate table to keep record of relationship, Naming convention uses model names alphabetically which means our table should be named `attribute_product` but you're free to use something else but I will stick to the conventions for now, let's create a new migration file.

```bash
php artisan make:migration create_attribute_product_table --create=attribute_product
```

Open your migration file and add these column to the schema
```php
Schema::create('attribute_product', function (Blueprint $table) {
    $table->bigIncrements('id');

    $table->unsignedBigInteger('attribute_id');
    $table->foreign('attribute_id')->references('id')->on('attributes');

    $table->unsignedBigInteger('product_id');
    $table->foreign('product_id')->references('id')->on('products');

    $table->unique(['attribute_id', 'product_id']);
});
```

And we are done here, now you can retrieve all attribute for a product using `$product->attributes` and all product with an attribute using `$attribute->product`.
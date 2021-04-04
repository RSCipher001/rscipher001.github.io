+++
categories = ["laravel", "queue"]
date = "2021-04-04"
description = "How to use queues in Laravel"
title = "How to Use Queues in Laravel"
+++

# Introduction

Concept of queues is awesome but learning queues can be little bit confusing for some users because you've to do a lot of things to get things working like create jobs and choose drivers and start queue workers but don't worry, when you will understand everything about queues life will be more easier. Let's get started

# Steps
- Choose a driver
- Create a table for queues
- Create a mail and sent it without queue(for demonstration)
- Create a job for sending mails in background
- Start queue worker
- Sending data to jobs

# Choose a driver
A driver defines how are we going to store and dispatch jobs in queues, don't worry about it we are going to use database for this post, you are free to use any other driver like `redis` but don't use `sync`, open your `.env` file and change `QUEUE_DRIVER` to `database`

# Create a table for queues
We will store queues in database so we need a table, To create queues table open terminal and type `php artisan queue:table` and then `php artisan migrate`, it will create jobs table in the database.

# Create a mail
We are going to use mail example so let's create a mail by running the following command
```bash
php artisan make:mail HelloMail -m mail.hello
````
and set mailtrap config in your `.env` file, to preview a mail without sending add this to your `web.php` and visit `/mail/hello`

```php
use App\Mail\HelloMail;

Route::get('mail/hello', function () {
	return (new HelloMail);
});
```

To send mail for testing add this lines to your web.php
```php
use App\Mail\HelloMail;
use Illuminate\Support\Facades\Mail;

Route::get('mail/hello/send', function () {
	Mail::to('johndoe@example.com')->send(new HelloMail);
});
```
If you will visit `/mail/hello/send` it will send an email synchronously so it will take some time, We are going to minimize that time  by creating a job that handles time consuming tasks in background.

You can also open tinker and type `Mail::to('johndoe@example.com')->send(new HelloMail);` to send mail.

# Create a job
To create a job run the following command in your terminal
```bash
php artisan make:job SendHelloEmail
```

now open `app/Jobs/SendHelloMail.php` and edit `handle()` method and copy paste the following code
```php
use App\Mail\HelloMail;
use Illuminate\Support\Facades\Mail;

public function handle()
{
	Mail::to('johndoe@example.com')->send(new HelloMail);
}
```
As you can see it is same line from `web.php` for sending email.

Now come back to your `web.php` and add these lines to create a new route that will send email by using job.
```php
use App\Jobs\SendHelloEmail;

Route::get('mail/hello/send/job', function () {
	dispatch(new SendHelloEmail);
});
```

and visit to `mail/hello/send/job` and it will add a new job for sending email but it will not send email, you can verify this by going to jobs table in the database.

# Start queue worker
To run the queue worker open terminal and type `php artisan queue:work` and it will start processing all pending jobs from jobs table, you can see output on the screen.

# Sending data to the jobs
In this example you can see that `johndoe@example.com` is hardcoded as email recipient but we need to pass it dynamically in real world apps, for that we are going to use Job constructor, I am not going to explain anything, following code snippet will do the job

```php
// web.php
use App\Jobs\SendHelloEmail;

Route::get('mail/hello/send/job', function () {
	dispatch(new SendHelloEmail('real-email@example.com'));
});
```

```php
// SendHelloEmail.php

protected $email;

public function __construct($email)
{
	$this->email = $email;
}

public function handle()
{
	Mail::to($this->email)->send(new HelloMail);
}
```

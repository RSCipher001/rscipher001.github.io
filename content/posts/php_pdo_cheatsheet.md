+++
categories = ["php"]
date = "2021-04-04"
description = "PHP PDO Cheatsheet"
title = "PHP PDO Cheatsheet"
+++

SQL injection is a big problem and prepared statement helps us protect from that, this is a collection of some code to perform basic tasks in PHP using PDO.

## Connection

`connection.php`
---
```php
$host = "localhost";
$username = "root";
$password = "";
$database = "training";
try
{
    $conn = new PDO("mysql:host=$host;dbname=$database", $username, $password);
    // set the PDO error mode to exception
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
}
catch(PDOException $e)
{
    echo "Connection failed: " . $e->getMessage();
    die();
}
```

## Select Data with Where Query
```php
$stmt = $conn->prepare()
```


```php
<?php

function precho($input)
{
    echo "<pre>";
    print_r($input);
    echo "</pre>";
}

$host = "localhost";
$username = "ravindra";
$password = "ravindra";
$database = "training";
try
{
    // Create a new PDO instrance
    $conn = new PDO("mysql:host=$host;dbname=$database", $username, $password);

    /**
     * Set error mode to exception,
     * You can also use ERRMODE_SILENT to ignore erros and
     * ERRMODE_WARNING to show errors as warnings.
     **/
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    
    /**
     * Sets default fetch to associative array mode
     * We can also use indexed array
     **/
    $conn->setAttribute(PDO::ATTR_DEFAULT_FETCH_MODE, PDO::FETCH_ASSOC);
}
catch(PDOException $e)
{
    // This code will only run when PDO will not be able to connect to the database
    // We can get error message with $e->message() function
    echo "Connection failed: " . $e->getMessage();
    die();
}

// Select multiple data with where condition

// Select id, name, email users with id greater than 1
$select_users_query = "SELECT id, name, email FROM users WHERE id > :id LIMIT 5";
$stmt = $conn->prepare($select_users_query);

// $stmt->bindParam(":id", 1);

$select_users_query_result = $stmt->execute([
    'id' => 1,
]);

if ($select_users_query_result)
{
    // Query Success

    // This will fetch array of array
    echo "<h1>Select Mutiple</h1>";
    // $users = $stmt->fetchAll();
    
    // Fetch as objects
    $users = $stmt->fetchAll(PDO::FETCH_CLASS);
    
    // print_r with pre tags to preserve formatting
    precho($users);
    echo "<hr>";
}
else
{
    // Query Failed
    echo "Query Failed";
    die();
}
$stmt = null;



// Select one with where condition

// Select id, name, email users with id greater than 1
$select_user_query = "SELECT id, name, email FROM users WHERE id > :id LIMIT 1";
$stmt = $conn->prepare($select_user_query);

$stmt->bindParam(":id", $a = '1');

// $select_users_query_result = $stmt->execute([
//     'id' => 1,
// ]);

$select_user_query_result = $stmt->execute();

if ($select_user_query_result)
{
    // Query Success

    // This will fetch array of array
    echo "<h1>Select Single</h1>";
    // $users = $stmt->fetchAll();
    
    // Fetch as objects
    $user = $stmt->fetchObject();
    
    // print_r with pre tags to preserve formatting
    precho($user);
    echo "<hr>";
}
else
{
    // Query Failed
    echo "Query Failed";
    die();
}

```

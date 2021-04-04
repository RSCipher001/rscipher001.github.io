+++
categories = ["php"]
date = "2021-04-04"
description = "PHP Cheatsheet"
title = "PHP Cheatsheet"
+++

PHP is really cool language, here are some snippet that can be used to speed your development.

# Count number of days in a month

```php
// February 2020
cal_days_in_month (CAL_GREGORIAN, 2, 2020);
```

# Get Day Name
```php
date('D');	// Thu
date('l');	// Thursday

// With argument
date('D', strtotime('2019-08-01'))	// Thu
date('l', strtotime('2019-08-01'))	// Thursday
```

# Get Day Number in Week
```php
date('N');	// 4 - Thursday

// With argument
date('N', strtotime('2019-08-01'))	// 4 - Thursday
```

# Time 12 Hour Format
```php
date('g:i A');	// 1:17 AM

// With argument
date('g:i A', strtotime('13:30:12 UTC'))	// 7:00 AM [Depends on current time zone settings]
```

# Code Igniter Remove `<p>` from validation messages
```php
$this->form_validation->set_error_delimiters('', '');
```

# Wordpress

## Enable Store Installation without FTP
add this line to config.
```php
define('FS_METHOD', 'direct');
```
# Create With - Laravel Models
A simple package that provides traits to add common indentity fields to Laravel
models when they are created. 

This package is designed to work out of the box with just the traits. No other
configuration is needed.

## Installation
**Dependencies**
- PHP 7
- Laravel 5.*

**Composer**
```
composer require joelshepherd/create-with
```

## Usage
Simply add the trait to your model that provides your desired field. If the
field is not empty and is unique in the database, it will be left unchanged.

### Create with UUID
Adds an unique UUID to the model.

**Default options**
- `getUuidField()` returns `uuid`

```php
<?php
use JoelShepherd\CreateWith;

class Example extends Model
{
    use CreateWith\Uuid;
}
```

```php
<?php

$example = Example::create();
$example->uuid; // 123e4567-e89b-12d3-a456-426655440000
```

### Create with slug
Adds an unique slug to the model. This can optionally be based on a text string
(like a title field on the model) and appended with a random slug if required
for uniqueness.

**Default options**
- `getSlugField()` returns `slug`
- `getSlugBaseText()` returns `null`
- `getSlugRandomLength()` returns `7`

```php
<?php
use JoelShepherd\CreateWith;

class Example extends Model
{
    use CreateWith\Slug;

    // Optionally set the base string to build the slug from
    protected function getSlugBaseText()
    {
        return $this->title;
    }
}
```

```php
<?php

// Creates a unique slug from the base text
$example = Example::create([
    'title' => 'This is a title'
]);
$example->slug; // this-is-a-title

// Uniqueness is retained even with the same base text
$example2 = Example::create([
    'title' => 'This is a title'
]);
$example2->slug; // this-is-a-title-7iw90lj
```

### Create with IP address
Adds the requester's IP address to the model.

**Default options**
- `getIpAddressField()` returns `ip_address`

```php
<?php
use JoelShepherd\CreateWith\WithIpAddress;

class Example extends Model
{
    use CreateWith\IpAddress;
}
```

```php
<?php

$example = Example::create();
$example->ip_address; // 127.0.0.1
```

## Contributing
Submitting issues and pull requests for bugs, features and feature requests are welcome.

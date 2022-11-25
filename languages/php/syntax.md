# PHP

## Classes & Objects

* You can instanciate objects in php without parentheses depending your constructor.
```php
$product = new Product;
```
* You need to set the access modifier for the attributes, by default the value of this properties is ``NULL``.
```php
// Product.class
class Product
{
  public $name;
  public $description;
}
```

* You can have typed properties and use ```strict_type``` declaration to catch bugs early on by restricting PHP to automatically cast primitive values. The default value for this variables is ``uninitialized`` and it will get an error if we try to access to the property.
```php
// Product.class
declare(strict_types=1)

class Product
{
  public string $name;
  public string $description;
}
```
* Use a constructor to initialize the values or properties, by default php assigns a ``public`` access modifier, though it is highly recommended to always set the access modifier to your methods to staty consistent and also it's better for readability.
```php
class Product
{
  public string $name;
  public string $description;
  public float $price;

  public function __construct($name, $description, $price)
  {
    $this->name = $name;
    $this->description = $description;
    $this->price = $price;
  }
}
```

* Since php 8 you can reduce the code at your constructor like:
```php
class Product
{
  public function __construct(private string $name,private string $description, private float $price)
  {
  }
}
```

* You can use the operator ```?``` before the a property's type class to set a ``null`` value.
```php
class Product
{
  public string $name;
  public string $description;
  public ?float $price; // using ? operator

  public function __construct($name, $description, $price)
  {
    $this->name = $name;
    $this->description = $description;
    $this->price = $price;
  }
}

$product = new Product('melon bread', 'so yummy', null);
```


### Importing a class

You can import a php class using: 
```php
require_once '../<classpath>/Product.php';
```

## Namespaces
You can use namespaces to avoid collisions between various classes with the same name.

PHP try get a class from a namespace in other case goes to check if it's present in the global space.

```php
namespace Store\Food;

class Product
{
  
}
```
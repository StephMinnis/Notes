## Set object properties
Properties - Class variables, attributes, fields
Public, Protected, Private
Inside methods:  $this->property
Outside methods: 

	1. Public:
		* $objectname->property = "some value";
		* $objectname->property;
	2. Private use getter/setter:
		* $object->setProperty("some value");
		* $object->getProperty;

## Class 
Recipe for an object

```php
<?php
class SimpleClass
{
    // property declaration
    public $var = 'a default value';

    // method declaration
    public function displayVar() {
        echo $this->var;
    }
}
```
[From] (https://www.php.net/manual/en/language.oop5.basic.php)


## Instantiating (Newing up) a class
Places handle (name) on an instance of the class that controls the instance of the object
``` 
    $bob = new person(); 
```
You can instantiate multiple objects by instantiating different handles

Static properties and methods do not need to be instantiated

## Getter/ Setter Methods
Method names reference the property they set

```php
<?php 
	class person {
		var $name; 
		function set_name($new_name) { 
			$this->name = $new_name;  
 		}
 
   		function get_name() {
			return $this->name;
		}
	} 
```
[From] (https://www.killerphp.com/tutorials/php-objects-page-1/)

## Constructors
Magic method that allows you to initialize things on instantiation

```php
<?php 		
	class person {
		var $name;
		function __construct($persons_name) {		
			$this->name = $persons_name;		
		}		  
	}

$bob = new person("bob"); 
```

[From] (https://www.killerphp.com/tutorials/php-objects-page-3/)

## Encapsulation: 
Public, Protected, Private
PUBLIC BY DEFAULT
* Public: Universally available with $object->property notation
* Protected: Only available inside class and child classes
* Private: Available in class only and must be accessed with getter/setter methods

Can be applied to properties and methods
Private methods can only be accessed by class methods in the class that contains them

## Inheritance 
- Reuse code by creating a child class that has traits of the parent
class employee extends person 
{
	function __construct($employee_name) {
		$this->set_name($employee_name);
	}
}
Employee is a type of person

## Overriding methods
Allows the child class or type to set its own methods done by declaring the same method in the child class

```php
<?php
	class person 
	{
		protected function set_name($new_name) {
			if ($new_name != "Jimmy Smith") {
				$this->name = strtoupper($new_name);
			}
		}
	} 
 
	class employee extends person 
	{
		protected function set_name($new_name) {
			if ($new_name == "Stefan Jones") {
				$this->name = $new_name;
			}
		}
	}
```

If you want to use the original method from the base class you use :: to set the correct method
	``` person::set_name($new_name); ```
Or if you just want to refer to the parent class (no name)
	``` parent::set_name($new_name); ```
	
[From] (https://www.killerphp.com/tutorials/php-objects-page-4/)


## Static variables:
Retain their value when jumping in and out of scope

```php
<?php
function test()
{
    static $a = 0;
    echo $a;
    $a++;
}
```

[From] (https://www.php.net/manual/en/language.variables.scope.php#language.variables.scope.static)

##Static methods: 
Can be accessed without instantiating the class
	-Since they aren't instantiated there is no $this

```php
<?php
class Foo {
    public static function aStaticMethod() {
        echo("Hello world");
    }
}

Foo::aStaticMethod();
$classname = 'Foo';
$classname::aStaticMethod();
```

[From] (https://www.php.net/manual/en/language.oop5.static.php)

## Static Properties:
Can't be accessed using ->

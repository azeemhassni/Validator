# PHP Server Side Form Validation



[![Build Status](https://travis-ci.org/azeemhassni/validator.svg?branch=v2.0)](https://travis-ci.org/azeemhassni/validator)
[![Codacy Badge](https://www.codacy.com/project/badge/333e9f1f4abf4f6195e4a99b1a2e5766)](https://www.codacy.com/app/azibaloch247/validator)
[![Latest Stable Version](https://poser.pugx.org/azi/validator/v/stable.svg)](https://packagist.org/packages/azi/validator) [![Total Downloads](https://poser.pugx.org/azi/validator/downloads.svg)](https://packagist.org/packages/azi/validator) [![Latest Unstable Version](https://poser.pugx.org/azi/validator/v/unstable.svg)](https://packagist.org/packages/azi/validator) [![License](https://poser.pugx.org/azi/validator/license.svg)](https://packagist.org/packages/azi/validator) 
[![Join the chat at https://gitter.im/azeemhassni/validator](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/azeemhassni/validator?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

This is a small PHP package that makes it easy to validate forms in your project specially larger forms.

[![Watch installation and basic usage](https://raw.githubusercontent.com/azeemhassni/validator/master/thumbnail.png)](http://www.youtube.com/watch?v=Ngxk95xg5DM)


## Installation Guide:

You can install **Validator** either via package download from github or via composer install. I encourage you to do the latter:
 
```json  
{ 
  "require": {
    "azi/validator": "1.*"
  }
} 
```


##Usage 
to get started 

* require composer autoloader 

```php
require 'vendor/autoload.php';
```

* Instantiate the Validator class
```php
use azi\Validator;
$v = new Validator();
```
* Define Rules for each form field
```php
  $rules = array(
        'name' => 'alpha|required',
        'age'  => 'num|required',
    );
```
* Run the **validator** 
```php
$v->validate( $_POST, $rules );
```
* check validator for errors, if validation fails redirect back to the form
```php
if ( !$v->passed() ) {
        $v->goBackWithErrors();
    }
```

* show validation errors to user
```html
 <label>Name :
      <input type="text" name="name">
 </label>
 <?=  Validator::error('name'); ?>
```

you can wrap error messages with custom HTML markup

```php
  Validator::error('confirm_password', '<span class="error">:message</span>');
```


## Rules
 * required
 * num
 * alpha
 * alnum
 * email
 * ip
 * url
 * min:number
 * max:number
 * same:field_name
 * array


## Custom Expressions & Messages
* Custom Expressions

you can register your custom RegExp before running the validator

```php
$v->registerExpression( 'cnic', '#^([0-9]{13})$#', 'Invalid CNIC number' );
```

registerExpression method takes 3 arguments
* expressionID - unique name for the expression
* pattern - the RegExp string
* message [optional] - the error message to be retured if the validation fails

```php 
Validator::registerExpression($expressionID , $pattern, $message)
```


* Custom Messages

you can also pass a custom error message with each rule

```php
 $rules['full_name'] = "required--Please Enter your name";
```

## Conditional Rules
you can spacify conditional rules for a field
```php
 $rules['age'] = 'if:gender[Male](required|min:2|num)';
```

## Comparison Rules

you can also compare a field with another
```php
  $rules['password'] = 'required|min:8';
  $rules['confirm_password'] = 'same:password';
```



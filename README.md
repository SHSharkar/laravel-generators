# laravel-generators

[![Latest Version on Packagist][ico-version]][link-packagist]
[![Software License][ico-license]](LICENSE.md)
[![StyleCI][ico-style-ci]][link-style-ci]
[![Build Status][ico-travis]][link-travis]
[![Coverage Status][ico-scrutinizer]][link-scrutinizer]
[![Quality Score][ico-code-quality]][link-code-quality]
[![Total Downloads][ico-downloads]][link-downloads]

This is a package developed by us for internal use. It is supposed to help us during development and save plenty of time by automating many steps while creating typical CRUD entities with [Laravel Backpack](https://laravel-backpack.readme.io/docs). You can write your own Services (they have to implement `Webfactor\Laravel\Generators\Contracts\ServiceInterface`) and register them in the `generators.php` config file, or use this package as an inspiration for your own implementation.

## Install

### Via Composer

This package is indended to be used only for development, not for production. Because of that we recommend to use `require-dev`:

``` bash
composer require-dev webfactor/laravel-generators
```

## Usage

``` bash
php artisan make:entity {entity_name} {--schema=} {--ide=}
```

`--schema` currently uses syntax from [Laravel 5 Extended Generators](https://github.com/laracasts/Laravel-5-Generators-Extended)

Use *singular* for entity. This will automatically create (while respecting our internal naming conventions):

* Migration
* Factory
* Seeder
* Backpack CRUD (modified Backpack Generator):
  * Model (incl. `$fillable`)
  * Request (incl. `rules()`)
  * Controller (incl. CrudColumns and CrudFields, basic for now)
* Language File
* Route to Backpack CRUD in admin.php

### Open files in IDE

With `{--ide=}` option you can define your preferred IDE to open all automatically generated files. This package comes with an implementation for PhpStorm (`Webfactor\Laravel\Generators\RecipesPhpStormOpener`) which is defined in `generators.php`. The keys in the `ides`-Array are possible values for the command option. You can add other IDE-Opener classes, they have to implement `Webfactor\Laravel\Generators\Contracts\OpenInIdeInterface`.`

In your service class you have to define the path to the file generated by this service. Then add `$this->addLatestFileToIdeStack();` and all files of the stack will be opened by `Webfactor\Laravel\Generators\Services\OpenIdeService`.

Example:

```php
<?php

class ExampleService extends ServiceAbstract implements ServiceInterface
{
    protected $relativeToBasePath = 'path/to/file';

    public function call()
    {
        // do some magic

        // searches for latest file (using modified date) in given directory and adds it to the stack
        $this->addLatestFileToIdeStack();
    }
}
```

## Adaption

Feel free to write your own Services that fit your purposes!

## Change log

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed recently.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) and [CODE_OF_CONDUCT](CODE_OF_CONDUCT.md) for details.

## Security

If you discover any security related issues, please email thomas.swonke@webfactor.de instead of using the issue tracker.

## Credits

- [Thomas Swonke][link-author]
- [All Contributors][link-contributors]

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.

[ico-version]: https://img.shields.io/packagist/v/webfactor/laravel-generators.svg?style=flat-square
[ico-license]: https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square
[ico-style-ci]: https://styleci.io/repos/125574603/shield
[ico-travis]: https://img.shields.io/travis/webfactor/laravel-generators/master.svg?style=flat-square
[ico-scrutinizer]: https://img.shields.io/scrutinizer/coverage/g/webfactor/laravel-generators.svg?style=flat-square
[ico-code-quality]: https://img.shields.io/scrutinizer/g/webfactor/laravel-generators.svg?style=flat-square
[ico-downloads]: https://img.shields.io/packagist/dt/webfactor/laravel-generators.svg?style=flat-square

[link-packagist]: https://packagist.org/packages/webfactor/laravel-generators
[link-style-ci]: https://styleci.io/repos/125574603
[link-travis]: https://travis-ci.org/webfactor/laravel-generators
[link-scrutinizer]: https://scrutinizer-ci.com/g/webfactor/laravel-generators/code-structure
[link-code-quality]: https://scrutinizer-ci.com/g/webfactor/laravel-generators
[link-downloads]: https://packagist.org/packages/webfactor/laravel-generators
[link-author]: https://github.com/tswonke
[link-contributors]: ../../contributors

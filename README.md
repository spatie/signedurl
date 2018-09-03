# Create secured URLs with a limited lifetime

[![Latest Version on Packagist](https://img.shields.io/packagist/v/spatie/url-signer.svg?style=flat-square)](https://packagist.org/packages/spatie/url-signer)
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.md)
[![Build Status](https://img.shields.io/travis/spatie/url-signer/master.svg?style=flat-square)](https://travis-ci.org/spatie/url-signer)
[![Quality Score](https://img.shields.io/scrutinizer/g/spatie/url-signer.svg?style=flat-square)](https://scrutinizer-ci.com/g/spatie/url-signer)
[![Total Downloads](https://img.shields.io/packagist/dt/spatie/url-signer.svg?style=flat-square)](https://packagist.org/packages/spatie/url-signer)

This package can create URLs with a limited lifetime. This is done by adding an expiration date and a signature to the URL.

```php
// Use MD5 URL signer class
$urlSigner = new MD5UrlSigner('randomkey');

$urlSigner->sign('https://myapp.com', 30);

// Use SH1 URL signer class
$urlSigner = new SH1UrlSigner('randomkey');

$urlSigner->sign('https://myapp.com', 30);

// => The generated url will be valid for 30 days
```

This will output an URL that looks like `https://myapp.com/?expires=xxxx&signature=xxxx`.

Imagine mailing this URL out to the users of your application. When a user clicks on a signed URL
your application can validate it with:

```php
$urlSigner->validate('https://myapp.com/?expires=xxxx&signature=xxxx');
```

Spatie is a webdesign agency in Antwerp, Belgium. You'll find an overview of all our open source projects [on our website](https://spatie.be/opensource).

## Postcardware

You're free to use this package (it's [MIT-licensed](LICENSE.md)), but if it makes it to your production environment we highly appreciate you sending us a postcard from your hometown, mentioning which of our package(s) you are using.

Our address is: Spatie, Samberstraat 69D, 2060 Antwerp, Belgium.

All postcards are published [on our website](https://spatie.be/en/opensource/postcards).

## Installation

The package can installed via Composer:
```
composer require spatie/url-signer
```

## Usage

A signer-object can sign URLs and validate signed URLs. A secret key is used to generate signatures.

```php
use Spatie\UrlSigner\MD5UrlSigner;

$urlSigner = new MD5UrlSigner('mysecretkey');
```

### Generating URLs

Signed URLs can be generated by providing a regular URL and an expiration date to the `sign` method.

```php
$expirationDate = (new DateTime)->modify('10 days');

$urlSigner->sign('https://myapp.com', $expirationDate);

// => The generated url will be valid for 10 days
```

If an integer is provided as expiration date, the url will be valid for that amount of days.

```php
$urlSigner->sign('https://myapp.com', 30);

// => The generated url will be valid for 30 days
```

### Validating URLs

To validate a signed URL, simply call the `validate()` method. This will return a boolean.

```php
$urlSigner->validate('https://myapp.com/?expires=1439223344&signature=2d42f65bd023362c6b61f7432705d811');

// => true

$urlSigner->validate('https://myapp.com/?expires=1439223344&signature=2d42f65bd0-INVALID-23362c6b61f7432705d811');

// => false
```

## Writing custom signers
This packages provides a signer that uses md5 and sh1 to generate signature. You can create your own
signer by implementing the `Spatie\UrlSigner\UrlSigner`-interface. If you let your signer extend
`Spatie\UrlSigner\BaseUrlSigner` you'll only need to provide the `createSignature`-method.

## Tests

The tests can be run with:

```
$ vendor/bin/phpspec run
```

## Integrations
To get started quickly in Laravel you can use the [spatie/laravel-url-signer](https://github.com/spatie/laravel-url-signer) package.

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## Security

If you discover any security related issues, please email freek@spatie.be instead of using the issue tracker.

## Credits

- [Sebastian De Deyne](https://github.com/sebastiandedeyne)
- [All Contributors](../../contributors)

## About Spatie

Spatie is a webdesign agency in Antwerp, Belgium. You'll find an overview of all our open source projects [on our website](https://spatie.be/opensource).

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.

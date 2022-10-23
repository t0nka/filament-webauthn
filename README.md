# Filament Webauthn Authentication (FIDO)

[![Latest Version on Packagist](https://img.shields.io/packagist/v/moontechs/filament-webauthn.svg?style=flat-square)](https://packagist.org/packages/moontechs/filament-webauthn)
[![GitHub Tests Action Status](https://img.shields.io/github/workflow/status/moontechs/filament-webauthn/run-tests?label=tests)](https://github.com/moontechs/filament-webauthn/actions?query=workflow%3Arun-tests+branch%3Amain)
[![GitHub Code Style Action Status](https://img.shields.io/github/workflow/status/moontechs/filament-webauthn/Fix%20PHP%20code%20style%20issues?label=code%20style)](https://github.com/moontechs/filament-webauthn/actions?query=workflow%3A"Fix+PHP+code+style+issues"+branch%3Amain)
[![Total Downloads](https://img.shields.io/packagist/dt/moontechs/filament-webauthn.svg?style=flat-square)](https://packagist.org/packages/moontechs/filament-webauthn)

Passwordless login for you Filament app. Webauthn server side and front-end components.

The package has the following components:
* registration button and widget
* login form extension to redirect to the webauthn login page
* separate route and page with webauthn login form

## Installation

You can install the package via composer:

```bash
composer require moontechs/filament-webauthn
```

You should publish and run the migrations with:

```bash
php artisan vendor:publish --tag="filament-webauthn-migrations"
php artisan migrate
```

You can publish the config file with:

```bash
php artisan vendor:publish --tag="filament-webauthn-config"
```

This is the contents of the published config file:

```php
return [
    'login_page_url' => '/webauthn-login',
    'user' => [
        'login_id' => 'email',
    ],
    'widget' => [
        'column_span' => '',
    ],
    'register_button' => [
        'icon' => 'heroicon-o-key',
        'class' => 'w-full',
    ],
    'login_button' => [
        'icon' => 'heroicon-o-key',
    ],
    'auth' => [
        'relying_party' => [
            'name' => env('APP_NAME'),
            'origin' => env('APP_URL'),
            'id' => env('APP_HOST', parse_url(env('APP_URL'))['host']),
        ],
        'client_options' => [
            'timeout' => 60000,
            'platform' => '', // available: platform, cross-platform, or leave empty
            'attestation' => 'direct', // available: direct, indirect, none
            'user_verification' => 'required', // available: required, preferred, discouraged
        ],
    ],
];
```

Optionally, you can publish the views using

```bash
php artisan vendor:publish --tag="filament-webauthn-views"
```

## Usage

* Install the package.
* Publish migrations and migrate.

### Add a registration widget
* Register `Moontechs\FilamentWebauthn\Widgets\WebauthnRegisterWidget::class` widget. 
Add it to  the `widgets.register` array of the Filament config.

Only signed-in users can register a device to be able to sign in using it in the future.

### Add just a registration button
* Add `<livewire:webauthn-register-button/>` in any view.

### Add a redirect to login page button
* Publish Filament login page view `php artisan vendor:publish --tag=filament-views`
* Add `<x-filament-webauthn::login-form-extension />` in the end of the login form.

## Testing

```bash
composer test
```

## Credits

- [Michael Kozii](https://github.com/mkoziy)
- [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.

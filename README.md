# Pennant for Filament

<p class="filament-hidden">
  <img src="https://raw.githubusercontent.com/maartenpaauw/pennant-for-filament-docs/main/assets/screenshots/banner.jpg" alt="Pennant for Filament">
</p>

## Introduction

Pennant for Filament is a powerful package that seamlessly integrates feature flags from Laravel Pennant into the
[Filament](https://filamentphp.com/) UI. With this package, managing and controlling feature flags becomes an effortless
task. Not only can you view and modify feature flags associated with the currently logged-in user, but you can also
manage feature flags for other users and models.

## Example

Consider a scenario where your application has feature flags like `New API` and `Site Redesign`. Occasionally, you need
to transition users to the new API. Traditionally, this would involve database operations. However, with Pennant for
Filament, you can perform these actions directly from Filament's user-friendly interface.

**This package empowers you to perform such actions with ease, all within Filament!**

### Demo Video

Check out this video demonstrating how straightforward it is to activate and deactivate feature flags using Filament:

[![Demo video](https://raw.githubusercontent.com/maartenpaauw/pennant-for-filament-docs/main/assets/screenshots/video.png)](https://www.youtube.com/watch?v=9quhtxAgHr4)

## Features

Pennant for Filament comes packed with a range of features to enhance your experience:

- List all Pennant feature flags within the default scope (logged-in user by default).
- List Pennant feature flags associated with a specific User model or other models.
- Seamlessly activate or deactivate feature flags.
- Easily manage rich feature flags.
- Filter feature flags based on various criteria.
  - Filter by status (active or inactive).
  - Display only rich feature flags.
- Enjoy translations support for feature flag names, resources, and relation managers.
- Leverage policy support for activating and deactivating feature flags.
- Compatible with dark mode.

## Screenshots

Take a glimpse of Pennant for Filament in action:

![Displaying all Pennant feature flags of the default scope](https://raw.githubusercontent.com/maartenpaauw/pennant-for-filament-docs/main/assets/screenshots/default-scope-resource.png)

_Displaying all Pennant feature flags of the default scope._

![Showcasing an overview of feature flags associated with a company](https://raw.githubusercontent.com/maartenpaauw/pennant-for-filament-docs/main/assets/screenshots/relation-manager.png)

_Showcasing an overview of feature flags associated with a company._

![Deactivating a feature flag](https://raw.githubusercontent.com/maartenpaauw/pennant-for-filament-docs/main/assets/screenshots/deactivate.png)

_Deactivating a feature flag._

![Activating a rich feature flag](https://raw.githubusercontent.com/maartenpaauw/pennant-for-filament-docs/main/assets/screenshots/activate-rich-feature-flag.png)

_Activating a rich feature flag._

![Filtering feature flags](https://raw.githubusercontent.com/maartenpaauw/pennant-for-filament-docs/main/assets/screenshots/filter-active-feature-flags.png)

_Filtering feature flags._

![Filtering rich feature flags](https://raw.githubusercontent.com/maartenpaauw/pennant-for-filament-docs/main/assets/screenshots/filter-rich-feature-flags.png)

_Filtering rich feature flags._

![Translated feature flags](https://raw.githubusercontent.com/maartenpaauw/pennant-for-filament-docs/main/assets/screenshots/dutch-translations.png)

_Translated feature flags._

![Feature flags that cannot be deactivated](https://raw.githubusercontent.com/maartenpaauw/pennant-for-filament-docs/main/assets/screenshots/policy.png)

_Feature flags that cannot be deactivated._

![Overview of feature flags in dark mode](https://raw.githubusercontent.com/maartenpaauw/pennant-for-filament-docs/main/assets/screenshots/darkmode.png)

_Overview of feature flags in dark mode._

## Installation

**Thank you for choosing Pennant for Filament!**

Here's a comprehensive guide to installing and utilizing this plugin. If you encounter any issues, have questions, need
support, or want to request a feature, please feel free to contact me at filamentphp@paauw.dev.

### Requirements

Pennant for Filament requires the following components:

- PHP `^8.1`
- Laravel `^10.0` or `^11.0`
- Laravel Pennant `^1.6`
- Filament `^3.2.39`

Additionally, make sure you have defined at least one feature flag in your project. For more information, refer to the
official Laravel [documentation](https://laravel.com/docs/10.x/pennant#defining-features).

### Installation steps

#### Install with Composer

To begin, add the private registry to your `composer.json`:

```json
{
  "repositories": [
    {
      "type": "composer",
      "url": "https://pennant-for-filament.composer.sh"
    }
  ]
}
```

Once the repository is added, you can install Pennant for Filament like any other composer package:

```shell
composer require maartenpaauw/pennant-for-filament
 
Loading composer repositories with package information
Authentication required (pennant-for-filament.composer.sh):
Username: [your-email]
Password: [your-license-key:your-domain]
```

You will be prompted to provide your username and password. The username will be your email address and the
password will be equal to your license key, followed by a colon (`:`), followed by the domain you are activating. For
example, let's say we have the following licensee and license activation:

- Contact email: `john.doe@example.com`
- License key: `8c21df8f-6273-4932-b4ba-8bcc723ef500`
- Activation fingerprint: `example.com`

This will require you to enter the following information when prompted for your credentials:

```shell
Loading composer repositories with package information
Authentication required (pennant-for-filament.composer.sh):
Username: john.doe@example.com 
Password: 8c21df8f-6273-4932-b4ba-8bcc723ef500:example.com
```

To clarify, the license key and fingerprint should be separated by a colon (`:`).

#### Publishing

The package offers English and Dutch translations. You can publish the language files if needed:

```shell
php artisan vendor:publish --tag="pennant-for-filament-translations"
```

#### Adding to panel

Integrate Pennant for Filament into your panel by instantiating the plugin class and passing it to the plugin method:

```php
public function panel(Panel $panel): Panel
{
    return $panel
    // ...
    ->plugin(
        \Maartenpaauw\Filament\Pennant\FilamentPennantPlugin::make(),
    );
}
```

### Deploying

It is not advised to store your `auth.json` file inside your project's version control repository. To store your
credentials on your deployment server you may create a Composer `auth.json` file in your project directory using the
following command:

```shell
composer config http-basic.pennant-for-filament.composer.sh your_account_email your_license_key:fingerprint_domain
```

You can see your credentials in your [Anystack.sh](https://anystack.sh/) account: Anystack -> Transactions -> View
details next to Pennant for Filament.

> [!IMPORTANT]
> Make sure the `auth.json` file is in `.gitignore` to avoid leaking credentials into your git history.

If you are using [Laravel Forge](http://forge.laravel.com/), you don't need to create the `auth.json `file manually.
Instead, you can set the credentials on the Composer Package Authentication screen of your server.

## Setup

### Resource

Once you've added `->plugin(FilamentPennantPlugin::make())` to your panel, a resource will automatically list the
feature flags of the logged-in user. To disable this resource, you can use the `->withoutResource()` method:

```php
public function panel(Panel $panel): Panel
{
    return $panel
    // ...
    ->plugin(
        \Maartenpaauw\Filament\Pennant\FilamentPennantPlugin::make()
            ->withoutResource(),
    );
}
```

### Relation Manager

While not mandatory, the relation manager is recommended for easy activation and deactivation of Pennant feature flags
for individual users. To use it, add a trait to the scope (e.g. `User`) model:

```php
class User extends Authenticatable
{
    // ...
    use \Maartenpaauw\Filament\Pennant\Concerns\HasFeatures;
    use \Laravel\Pennant\Concerns\HasFeatures;
    
    // ...
}
```

Finally, add the relation manager to the `getRelations()` array:

```php
public static function getRelations(): array
{
    return [
        \Maartenpaauw\Filament\Pennant\Resources\FeatureResource\RelationManagers\FeatureRelationManager::class,
    ];
}
  ```

### Rich features

For projects that employ rich feature flags, enabling users to select values during feature flag activation is
essential. By implementing the `RichFeature` interface and providing the desired options, a select input will appear
within the confirmation pop-up, streamlining the process.

Here's an example implementation:

```php
<?php

namespace App\Features;

use Illuminate\Support\Collection;

class PurchaseButton implements \Maartenpaauw\Filament\Pennant\Contracts\RichFeature
{
    public function resolve(mixed $scope): string
    {
        return 'blue-sapphire';
    }

    public function options(mixed $scope): Collection
    {
        return Collection::make([
            'blue-sapphire' => 'Blue Sapphire',
            'sea-foam-green' => 'Sea Foam Green',
            'tart-orange' => 'Tart Orange',
        ]);
    }
}
```

### Policy

If you need to restrict feature flag activation or deactivation to specific users, you can implement
a [Policy](https://laravel.com/docs/10.x/authorization#creating-policies). To begin, create a `FeaturePolicy` and
include it in the `$policies` array as you would with any other policy.

Since feature flags typically involve activation and deactivation, the custom methods `activate` and `deactivate` are
utilized:

```php
<?php

namespace App\Policies;

class FeaturePolicy
{
    public function activate(User $user, \Maartenpaauw\Filament\Pennant\Models\Feature $feature): bool
    {
        return true;
    }

    public function deactivate(User $user, \Maartenpaauw\Filament\Pennant\Models\Feature $feature): bool
    {
        return false;
    }
}
```

> [!WARNING]
> Ensure that you're using the `Feature` model from the package and not the `Feature` facade from Pennant itself.

### Translations

Pennant for Filament offers translation support for multiple languages. While English and Dutch are included by default,
you can extend this support for other languages. For instance, to add Spanish translations, create a `labels.php` file
under `lang/vendor/pennant-for-filament/es/` with the necessary translations:

```php
<?php

return [
    'activate' => 'Activar',
    'active' => 'Activa',
    'deactivate' => 'Desactivar',
    'feature' => 'Característica',
    'features' => 'Características',
    'inactive' => 'Inactivo',
    'name' => 'Nombre',
    'rich_features' => 'Características ricas',
    'status' => 'Estado',
    'value' => 'Valor',
];
```

To translate feature names, create a translation file in the `lang` directory (e.g., `nl.json`) for translation:

```json
{
  "New Api": "Nieuwe API",
  "Purchase Button": "Koop knop",
  "Site Redesign": "Site herontwerp",
  "Teams": "Teams",
  "User Management": "Gebruikersbeheer"
}
```

> [!TIP]
> When the `HasLabel` interface is implemented, the return value of method `getLabel` is used as feature name.

## Need Assistance?

Questions, bugs, feature requests, or suggestions? Feel free to contact me at filamentphp@paauw.dev. Your feedback is
invaluable.

## Licensing Information

### Single License

The single license permits the use of Pennant for Filament in a single project hosted on a single domain or subdomain.
It's suitable for personal websites or client-specific websites.

For SaaS applications, you'll require an unlimited license.

### Unlimited License

The unlimited license allows the usage of Pennant for Filament on multiple domains, subdomains, and even in SaaS
applications.

### Code Distribution

Please note that the licenses for Pennant for Filament prohibit the public distribution of its source code. Hence, you
cannot build and distribute applications using Pennant for Filament's source code on open-source platforms.

### Questions About Licensing?

If you're uncertain about which license is appropriate for your needs, don't hesitate to reach out. Contact me at
filamentphp@paauw.dev, and I'll be glad to assist you.

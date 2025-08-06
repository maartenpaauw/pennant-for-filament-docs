# Pennant for Filament

<p class="filament-hidden">
  <a href="https://checkout.anystack.sh/pennant-for-filament">
    <img src="https://raw.githubusercontent.com/maartenpaauw/pennant-for-filament-docs/main/assets/screenshots/banner.jpg" alt="Pennant for Filament">
  </a>
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

![Feature flags user menu item](https://raw.githubusercontent.com/maartenpaauw/pennant-for-filament-docs/main/assets/screenshots/user-menu-item.png)

_Feature flags user menu item._

![Feature flags tenant menu item](https://raw.githubusercontent.com/maartenpaauw/pennant-for-filament-docs/main/assets/screenshots/tenant-menu-item.png)

_Feature flags tenant menu item._

![Overview of feature flags in dark mode](https://raw.githubusercontent.com/maartenpaauw/pennant-for-filament-docs/main/assets/screenshots/darkmode.png)

_Overview of feature flags in dark mode._

## Installation

**Thank you for choosing Pennant for Filament!**

Here's a comprehensive guide to installing and utilizing this plugin. If you encounter any issues, have questions, need
support, or want to request a feature, please feel free to contact me at filamentphp@paauw.dev.

### Requirements

Pennant for Filament requires the following components:

- PHP `^8.2`
- Laravel `^11.0` or `^12.0`
- Laravel Pennant `^1.16`
- Filament `^4.0`

Additionally, make sure you have defined at least one feature flag in your project. For more information, refer to the
official Laravel [documentation](https://laravel.com/docs/12.x/pennant#defining-features).

### Installation Steps

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

#### Adding to a Panel

Integrate Pennant for Filament into your panel by instantiating the plugin class and passing it to the plugin method:

```php
public function panel(Panel $panel): Panel
{
    return $panel
    // ...
    ->plugin(
        \Maartenpaauw\Filament\Pennant\Infrastructure\Filament\FilamentPennantPlugin::make(),
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

### Null Scope Feature Flags Page

In addition to user-specific and tenant-specific feature flags, you may want to manage global feature flags that are not
tied to any specific user or model. These are known as "null scope" feature flags in Laravel Pennant.

The package provides a dedicated page for viewing and managing these global feature flags. Unlike the user and tenant
feature flag pages, this page is not automatically registered by the plugin and must be manually added to your panel.

To enable the null scope feature flags page, add the `ListAllFeatureFlagsForNullScopePage` class to your panel's pages:

```php
public function panel(Panel $panel): Panel
{
    return $panel
    ->plugin(
        \Maartenpaauw\Filament\Pennant\Infrastructure\Filament\FilamentPennantPlugin::make(),
    )
    ->pages([
        \Maartenpaauw\Filament\Pennant\Infrastructure\Filament\Pages\ListAllFeatureFlagsForNullScopePage::class,
    ]);
}
```

### Disable Current User Feature Flags

This package automatically adds a feature flags menu item to the user's menu and displays feature flags in a table
format. If you wish to hide this menu item and its associated page, you can disable this functionality when configuring
the plugin.

```php
public function panel(Panel $panel): Panel
{
    return $panel
    // ...
    ->plugin(
        \Maartenpaauw\Filament\Pennant\Infrastructure\Filament\FilamentPennantPlugin::make()
            ->withoutUserFeatureFlags(),
    );
}
```

### Disable Current Tenant Feature Flags

This package automatically adds a feature flags menu item to the tenant's menu and displays feature flags in a table
format, when the plugin detects the panel has tenancy configured. If you wish to hide this menu item and its associated
page, you can disable this functionality when configuring the plugin.

```php
public function panel(Panel $panel): Panel
{
    return $panel
    // ...
    ->plugin(
        \Maartenpaauw\Filament\Pennant\Infrastructure\Filament\FilamentPennantPlugin::make()
            ->withoutTenantFeatureFlags(),
    );
}
```

### Display Record's Feature Flags

When working with feature flags that are scoped to specific records (like users, teams, or other models), you may want
to display these feature flags directly on the record's edit or view pages. This provides a convenient way to see and
manage feature flags associated with a particular record.

To display a record's feature flags, you can add the `ListAllFeatureFlagsForScopeWidget` as a footer widget in your
resource pages. This widget will show a table of all feature flags and their status for the current record.

For example, to display feature flags on an `EditUser` or `ViewUser` page, add the following method to your resource
page class:

```php
protected function getFooterWidgets(): array
{
    return [
        Maartenpaauw\Filament\Pennant\Infrastructure\Filament\Widgets\ListAllFeatureFlagsForScopeWidget::make([
            'scope' => $this->getRecord(),
        ])
    ];
}
```

### Rich Features

For projects that employ rich feature flags, enabling users to select values during feature flag activation is
essential. By implementing the `RichFeature` interface and providing the desired options, a select input will appear
within the confirmation pop-up, streamlining the process.

Here's an example implementation:

```php
<?php

namespace App\Features;

use Illuminate\Support\Collection;

final readonly class PurchaseButton implements \Maartenpaauw\Filament\Pennant\Infrastructure\Pennant\RichFeature
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
a [Policy](https://laravel.com/docs/12.x/authorization#creating-policies). To begin, create a `FeaturePolicy` and
include it in the `$policies` array as you would with any other policy.

Since feature flags typically involve activation and deactivation, the custom methods `activate` and `deactivate` are
used:

```php
<?php

namespace App\Policies;

use Maartenpaauw\Filament\Pennant\Domain\FeatureFlag;

class FeaturePolicy
{
    public function activate(User $user, FeatureFlag $featureFlag): bool
    {
        return true;
    }

    public function deactivate(User $user, FeatureFlag $featureFlag): bool
    {
        return false;
    }
}
```

### Translations

Pennant for Filament offers translation support for multiple languages. While English and Dutch are included by default,
you can extend this support for other languages. For instance, to add Spanish translations, create a `labels.php` file
under `lang/vendor/pennant-for-filament/fr/` with the necessary translations:

```php
<?php

return [
    'activate' => 'Activer',
    'active' => 'Actif',
    'activated' => 'Activé',
    'deactivate' => 'Désactiver',
    'deactivated' => 'Désactivé',
    'feature_flags' => 'Indicateurs de fonctionnalité',
    'inactive' => 'Inactif',
    'name' => 'Nom',
    'rich_feature_flags' => 'Indicateurs de fonctionnalité enrichis',
    'status' => 'Statut',
    'value' => 'Valeur',
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

### Single Project License

The Single Project license allows for the utilization of Pennant for Filament within a single project hosted on
one domain or subdomain. It is suitable for personal websites or websites tailored to specific clients.

If you intend to incorporate Pennant for Filament into a SaaS application, you must obtain an Unlimited Projects or
Lifetime license.

Under the Single Project license, you are authorized to activate Pennant for Filament up to 4 times (development,
test, staging and production).

You will receive updates and bug fixes for one year from the purchase date. If you choose not to renew your license, you
can only install the plug-in up to the latest version available before the license expiration. Renewing the license at a
discounted rate allows you to continue receiving updates and new features.

### Unlimited Projects License

The Unlimited Projects license permits the utilization of Pennant for Filament across multiple domains, subdomains,
and even in SaaS applications.

You will receive updates and bug fixes for one year from the purchase date. If you choose not to renew your license, you
can only install the plug-in up to the latest version available before the license expiration. Renewing the license at a
discounted rate allows you to continue receiving updates and new features.

### Lifetime License

The Lifetime License affords the licensee the same privileges as the Unlimited License.

You will receive updates for the lifetime of the product.

### Code Distribution

Please note that the licenses for Pennant for Filament prohibit the public distribution of its source code. Hence, you
cannot build and distribute applications using Pennant for Filament's source code on open-source platforms.

### Questions About Licensing?

If you're uncertain about which license is appropriate for your needs, don't hesitate to reach out. Contact me at
filamentphp@paauw.dev, and I'll be glad to assist you.

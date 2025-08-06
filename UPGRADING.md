# Upgrade Guide

## Version 2.0.0

This guide will help you upgrade from version `1.x` to version `2.0.0`. This is a major release with several breaking changes that require manual intervention.

### Before You Start

> [!WARNING]
> Version 2.0.0 introduces significant breaking changes. Please review this guide carefully and test your upgrade in a development environment first.

**Backup:** Always back up your application before upgrading.

### Step 1: Update Dependencies

Update your `composer.json` to require the new version:

```bash
composer require maartenpaauw/pennant-for-filament:^2.0
```

### Step 2: Update Translation Keys

Several translation keys have been renamed. Update your language files:

#### Required Changes

- Rename `features` to `feature_flags`
- Rename `rich_features` to `rich_feature_flags`
- Remove the `feature` translation key (no longer used)
- Add new `activated` and `deactivated` translation keys

**Example translation file updates:**

```php
// Before (v1.x)
'features' => 'Features',
'rich_features' => 'Rich Features',
'feature' => 'Feature',

// After (v2.0)
'feature_flags' => 'Feature Flags',
'rich_feature_flags' => 'Rich Feature Flags',
'activated' => 'Activated',
'deactivated' => 'Deactivated',
```

### Step 3: Remove Deprecated Trait

If you were using the `HasFeatures` trait, remove it from your models:

```php
use Maartenpaauw\Filament\Pennant\Concerns\HasFeatures;

// Remove this trait usage from your models
use HasFeatures;
```

### Step 4: Update Namespace Imports

Several classes have been moved to new namespaces. Update your imports:

#### The `RichFeature` interface
```php
// Before
use Maartenpaauw\Filament\Pennant\RichFeature;

// After
use Maartenpaauw\Filament\Pennant\Infrastructure\Pennant\RichFeature;
```

#### The `FilamentPennantPlugin` class
```php
// Before
use Maartenpaauw\Filament\Pennant\FilamentPennantPlugin;

// After
use Maartenpaauw\Filament\Pennant\Infrastructure\Filament\FilamentPennantPlugin;
```

#### The `FilamentPennantServiceProvider` class
```php
// Before
use Maartenpaauw\Filament\Pennant\FilamentPennantServiceProvider;

// After
use Maartenpaauw\Filament\Pennant\Infrastructure\Illuminate\FilamentPennantServiceProvider;
```

### Step 5: Replace Removed Components

Several Filament components have been removed and replaced with new alternatives.

#### Feature Resource Replacement

The `FeatureResource` has been removed. Listing the current user or current tenant feature flags is automatically enabled. Those pages can be found via the user menu or tenant menu. If you would like to list all `null` scope feature flags, you should register the `ListAllFeatureFlagsForNullScopePage` page within your panel configuration:

```php
public function panel(Panel $panel): Panel
{
    return $panel
        ->pages([
            ListAllFeatureFlagsForNullScopePage::class,
        ]);
}
```

#### FeatureRelationManager Replacement

The relation manager has been removed because feature flags aren't resolved using a relationship anymore. Therefore, you should replace `FeatureRelationManager` with the newly introduced widget classes. For example, if you would like to display a user's feature flags on their edit page, you should add the following code to the `EditUser` page:

```php
protected function getFooterWidgets(): array
{
    return [
        ListAllFeatureFlagsForScopeWidget::make([
            'scope' => $this->getRecord(),
        ])
    ];
}
```

### Step 6: Remove Deprecated Methods

Remove any usage of the `withoutResource()` method:

```php
FilamentPennantPlugin::make()
    ->withoutResource() // Remove this line
```

### Step 7: Remove Model References

If you were directly using the `Feature` model in your code, remove these references:

```php
// Remove any direct usage of:
use Maartenpaauw\Filament\Pennant\Feature;
```

### Step 8: Choose Your Display Components

Version 2.0 provides more granular control over how feature flags are displayed. Choose the appropriate components for your needs:

#### Pages Available:
- `ListAllFeatureFlagsPage` - Base page for listing feature flags that can be extended to implement your own scope logic.
- Tenant-specific feature flags page
- User-specific feature flags page
- Null scope feature flags page

#### Widgets Available:
- `ListAllFeatureFlagsWidget` - Base widget for listing feature flags that can be extended to implement your own scope logic.
- Tenant-specific feature flags widget
- User-specific feature flags widget
- Null scope feature flags widget

### Step 9: Update Your Custom Created Policy

If you created custom policy classes and referenced the `\Maartenpaauw\Filament\Pennant\Models\Feature` class, you must update it to use the `Maartenpaauw\Filament\Pennant\Domain\FeatureFlag` class. To receive the feature flag's scope, you should call the following code within your policy:

```php
<?php

namespace App\Policies;

use Illuminate\Foundation\Auth\User;
use Maartenpaauw\Filament\Pennant\Domain\FeatureFlag;

class FeaturePolicy
{
    public function activate(User $user, FeatureFlag $featureFlag): bool
    {
        return $user->is($featureFlag->scope->unwrap());
    }
}
```

### Step 10: Test Your Application

After completing the upgrade:

1. Clear your application cache: `php artisan cache:clear`
2. Clear your config cache: `php artisan config:clear`
3. Clear your view cache: `php artisan view:clear`
4. Test all feature flag functionality
5. Verify that your custom translations are working
6. Check that your Filament pages and widgets display correctly

### Troubleshooting

#### Common Issues

**Translation keys not found:** Make sure you've updated all translation files with the new key names.

**Class not found errors:** Double-check that you've updated all namespace imports according to Step 4.

**Missing feature flag displays:** Ensure you've replaced the removed components with their new equivalents from Steps 5 to 7.

**Authorization issues:** If you're having permission problems, consider implementing the new `FeatureFlagPolicy` from Step 9.

### Getting Help

If you encounter issues during the upgrade:

1. Check that you've followed all steps in this guide
2. Review the changelog for additional context
3. Check the package documentation for the latest examples

### Summary

Version `2.0.0` removes the Laravel Sushi dependency and provides more flexible, granular control over feature flag display. While this upgrade requires several manual changes, the new architecture provides better performance and more customization options.

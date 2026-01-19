# Changelog

## 2.0.2 - 2026-01-19

### Added

- Support for Filament version 5.

## 2.0.1 - 2025-12-30

### Added

- Support for PHP version 8.5.
- Support for Webmozart's assert version 2.

## 2.0.0 - 2025-08-15

### Added

- Support for Filament version 4
- Translation keys for `activated` and `deactivated` states
- Dedicated Filament pages for viewing feature flags:
  - Current tenant's feature flags
  - Current user's feature flags
  - Feature flags with null scope
  - Base page for any scope's feature flags
- Filament table widgets for displaying feature flags:
  - Current tenant's feature flags widget
  - Current user's feature flags widget
  - Null scope feature flags widget
  - Base widget for any scope's feature flags
- Default `FeatureFlagPolicy` class for simplified activation and deactivation permissions

### Changed

- Translation key updates:
  - `features` → `feature_flags`
  - `rich_features` → `rich_feature_flags`
- Namespace reorganization for better structure:
  - `RichFeature` contract moved to `Maartenpaauw\Filament\Pennant\Infrastructure\Pennant`
  - `FilamentPennantPlugin` moved to `Maartenpaauw\Filament\Pennant\Infrastructure\Filament`
  - `FilamentPennantServiceProvider` moved to `Maartenpaauw\Filament\Pennant\Infrastructure\Illuminate`

### Removed

- Support for Filament version 3
- **Translation keys:**
  - `feature` translation key
- **Traits and dependencies:**
  - `HasFeatures` trait
  - Laravel Sushi dependency (replaced with Filament's custom data records)
- **Configuration methods:**
  - `withoutResource()` method (feature flag resource no longer exists)
- **Models:**
  - `Feature` model (was internal-only but may affect external usage)
- **Filament components:**
  - `FeatureResource` page → use new page classes or extend `ListAllFeatureFlagsPage`
  - `ListFeature` page → use new page classes or extend `ListAllFeatureFlagsPage`
  - `FeatureRelationManager` → use new widget classes or extend `ListAllFeatureFlagsWidget`

* setup package 
# Filament language switcher (Localization)
https://github.com/bezhanSalleh/filament-language-switch


# Spatie role and permissions
https://filamentphp.com/plugins/bezhansalleh-shield

* **defined it in admin panel** 

```
 ->plugins([ \Filament\SpatieLaravelTranslatablePlugin::make()->defaultLocales(['ar','en']),
```

* in create resource 
```
use CreateRecord\Concerns\Translatable;
 
    protected function getHeaderActions(): array
    {
        return [
            Actions\LocaleSwitcher::make(),
             
        ];
    }
```

* in edit resource 
```
 use EditRecord\Concerns\Translatable;

    Actions\LocaleSwitcher::make(),

```
* in edit resource 
```
 use EditRecord\Concerns\Translatable;

    Actions\LocaleSwitcher::make(),

```
* in list resource
```
    use ListRecords\Concerns\Translatable;

    Actions\LocaleSwitcher::make(),
```

* use in model 
```
use Spatie\Translatable\HasTranslations;

use HasTranslations;
 protected $translatable =['name'];

```

* use in resource
```
use Filament\Resources\Concerns\Translatable;
    use Translatable;
```

* translated releationship manager

```
  public static function getTitle(Model $ownerRecord, string $pageClass): string
    {
        return __('user.images');
    }

    public static function getModelLabel(): string
    {
        return __('user.more');
    }
```

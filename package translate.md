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
* translate field  in sidebar and model label
* in resource 
```
 public static function getNavigationLabel(): string
    {
        return __(' ');
    }
    public static function getModelLabel(): string
    {
        return __(' ');
    }
    public static function getNavigationGroup(): string
    {
       return __(' ');
    }
    public static function getPluralModelLabel(): string
    {
        return __(' ');
    }

* get count by livewire 
    public static function getNavigationBadge(): ?string
    {
        return Model::count();
    }
  ```

* in custom pages
```
 * translate heading in custom page

    public function getHeading(): string{
        return __('pages.home');
    }
```
 * translate any title in custom page 
```
  public function getTitle(): string | Htmlable{
        return __('pages.home');
    }
```
  

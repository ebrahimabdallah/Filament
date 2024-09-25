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
        return __('filament-panels::pages/dashboard/user.RetrievalMaterial');
    }
```
 * translate any title in custom page 
```
  public function getTitle(): string | Htmlable{
        return __('filament-panels::pages/dashboard/labels.retrieval_materials');
    }
```
  

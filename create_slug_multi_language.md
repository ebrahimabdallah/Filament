* **filamnet slug** 
```

  TextInput::make('name')
                           
    ->required()
       ->label(__('pages.name'))
       ->validationMessages([
            'required' => __('validation.required'),
          ])->live(onBlur:false)->reactive()
            ->afterStateUpdated(function ($get, $set) {
                $name = $get('name');
                $name_slug=Product::slug($name);
                $set('slug', $name_slug);  
          }),
                                      
      Forms\Components\TextInput::make('slug')->readOnly(),                       
              
```

* **in Model**
* **ar , en**
```
public static function slug($string, $separator = '-')
{
    if (is_null($string)) {
        return "";
    }

    $string = trim($string);
    $string = mb_strtolower($string, "UTF-8");

    // Replace slashes
    $string = str_replace(['/', '\\'], $separator, $string);
    
    // Remove unwanted characters
    $string = preg_replace("/[^a-z0-9_\sءاأإآؤئبتثجحخدذرزسشصضطظعغفقكلمنهويةى]/u", "", $string);
    
    // Reduce spaces to a single separator
    $string = preg_replace("/[\s-]+/", " ", $string);
    
    // Replace spaces with the separator
    $string = preg_replace("/[\s_]/", $separator, $string);

    return $string;
}
    
```
* thanks : eng : bassem allam 

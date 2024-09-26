* **infolist**

```
   public static function infolist(Infolist $infolist): Infolist
    {
        return $infolist
            ->schema([
                Infolists\Components\TextEntry::make('user.name')
                ->label(__('forms.name'))
                  
            ]);
    }

```
* create nice list to show data
* image after use it 
![image](https://github.com/user-attachments/assets/c791169e-5e20-4d20-9abf-d728fee38515)

* image before

![Screenshot 2024-09-26 154004](https://github.com/user-attachments/assets/4f22fbce-2c9d-472a-840e-536975fbc989)

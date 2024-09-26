* **image explane case** 

![Screenshot 2024-09-25 091946](https://github.com/user-attachments/assets/a537f100-9ab5-4fd5-ab78-6d5e900f525f)



```
 public function getTabs(): array
    {
        return [
            'all' => Tab::make('all')
            ->label(__('pages.all'))
            ->query(fn (Builder $query): Builder => $query)
            ->icon('heroicon-o-calendar'),

            
            'today' => Tab::make('today')  //name of tabs 
                ->label(__('pages.today'))  //translated it
                // query to filter by it
                ->modifyQueryUsing(function (Builder $query): Builder {
                    return $query->whereDate('column you want to filter by ', today());  //you can replace it whereDate by where or any condition statument based on cases 
                })
                ->icon('heroicon-o-sun'),
        ];
    }
```
* **in table if have enum status you need show it and translated 
```
 ->formatStateUsing(fn ($state) => $state ? __('forms.inside') : __('forms.outside')),

```

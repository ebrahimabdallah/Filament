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

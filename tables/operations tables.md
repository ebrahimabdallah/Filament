* to make any operations and write login  in table button
```
->afterStateUpdated(function ($state, $record) {
// add logic 
}
```
* filter data table 

```
 ])->modifyQueryUsing(function (Builder $query) {
                return $query->where('type', '2');
})->defaultSort('created_at', 'desc')
```

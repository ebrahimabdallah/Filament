* How to Custom attributes

```
->extraAttributes(['class' => 'bg-gray-200'])

```

```
->extraAttributes(function (?Model $record) {
    $bgColor = Status::where('id', $record->status_id)->first()->color ?? 'white';
    return ['style' => "background-color: {$bgColor};"];
}),

```
 
* formating coulmn in table 
```
  TextEntry::make('status')
  ->badge()  // Optionally display the badge style
  ->formatStateUsing(function ($state) {
      return $state == 1 ? __('Active') : __('Inactive');
  })
  ->label(__('admin.status')),

```

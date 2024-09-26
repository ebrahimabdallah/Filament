
* **Select Options** 

```
  Select::make('test_id')
          ->label(__('translated'))
          ->options(Model::pluck('name', 'id')->toArray())
          ->searchable() // to search in 
          ->required(), //validation 
          ->validationMessages([ 'required' => __('validation.required'), ]) //message validation 
```


* **Repeater**

![image](https://github.com/user-attachments/assets/48d42816-85ef-489e-9e93-3fd36f7197e3)


  ```
 Repeater::make('members')
    ->schema([
        TextInput::make('name')->required(),
        Select::make('role')
            ->options([
                'member' => 'Member',
                'administrator' => 'Administrator',
                'owner' => 'Owner',
            ])
            ->required(),
    ])
    ->columns(2)
```
* **Reordering items in a relationship**
```
Repeater::make('qualifications')
    ->relationship()
    ->schema([
        // ...
    ])
    ->orderColumn('order_column')
```
* link
https://filamentphp.com/docs/3.x/forms/fields/repeater

* **Sections**
* **image expline case**
  ![image](https://github.com/user-attachments/assets/a74c9a52-17f2-43b2-a91e-17393b53cce5)

* to add smart style in forms 
```
 ->schema([
            Section::make(__('name of form'))
            ->description(__('desc_form'))
            ->schema([
         // code of form 
])

* link
https://filamentphp.com/docs/3.x/infolists/layout/section
```

* **image upload**
```
  Forms\Components\FileUpload::make('test_image')
                    ->label(__('forms.test_image')) 
                    ->directory('uploads/images/car') // store in path
                    ->validationMessages([
                        'required' => __('validation.required'),
                    ]), // validation 
```

* **RichEditor Input** 
![image](https://github.com/user-attachments/assets/89083c7d-e90b-4285-a783-a7fd09d3cb3f)
```
 RichEditor::make('content')
  ->toolbarButtons([
        'attachFiles',
        'blockquote',
        'bold',
.etc...
```











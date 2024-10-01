# Filament
* **Filament** is a popular package for Laravel that provides a beautiful and flexible admin panel to manage data in Laravel applications. It helps developers quickly build interactive dashboards, CRUD (Create, Read, Update, Delete) interfaces, and other administrative tools with ease.

* **Admin Panel**: It generates a user-friendly admin interface to manage your application’s data.
* **CRUD Resources**: Filament makes it easy to create and manage CRUD functionality with its Resources. It auto-generates forms, tables, and filters.
* **Custom Forms**: Filament provides powerful form builders that allow you to create custom forms with inputs like text, select, file uploads, and more.
* **Table Components**: It includes table components that enable you to list and manipulate data with pagination, sorting, and searching.
* **Widgets and Dashboard**: You can build custom widgets and dashboards to display reports or key metrics.
* **Access Control**: Built-in user role and permission system to manage access control within the admin panel.
* **Custom Actions**: You can add custom buttons and actions to your forms and tables, such as exporting data, bulk operations, or custom workflows.
* https://filamentphp.com/docs/3.x/actions/prebuilt-actions/create
* **Custom Page** if you need write code or create pages special hard logic out resource you can make a suctom page such :- print screen ..
# Installation
```
composer require filament/filament:"^3.2" -W
 
php artisan filament:install --panels
```
* **Create a user**
```
php artisan make:filament-user
```


# Managing relationships

```
php artisan make:filament-relation-manager CategoryResource posts title
```
* CategroyResource is name resource To which the relationship is developed
* posts name of the relationship you want to manage (name in model....).
* title attribute that will be used to identify posts.

* if you have BelongsToMany and MorphToMany relationships.
```
php artisan make:filament-relation-manager CategoryResource posts title --attach
```

* Viewing related records
* you may pass the --view flag to also add a ViewAction to the table:
```
php artisan make:filament-relation-manager CategoryResource posts title --view
```
  
# Custom Page 

* SortUsers name page
* User resource To which the custom is developed
```
php artisan make:filament-page SortUsers --resource=UserResource --type=custom
```
* create Filamnet Provider and register in 
```
php artisan make:provider FilamnetProvider 
```
* You must register custom pages to a route in the static getPages() method of your resource:
```
'sort' => Pages\SortUsers::route('/sort'),
```


# Repeater

* repeater component allows you to output a JSON array of repeated form components.

```
Repeater::make('members')
    ->schema([
        // ...
    ])
```
* Repeaters may have a certain number of empty items created by default,
```
->defaultItems(3)
```
* You may prevent the user from adding items to the repeater 
```
->addable(false)
```
* You may prevent the user from deleting items from the repeater 
```
 ->deletable(false)
```
* You may prevent the user from reordering items from the repeater
```
->reorderable(false)
```

* Preventing reordering with drag and drop
```
 ->reorderableWithDragAndDrop(false)
```
* **Integrating with an Eloquent relationship**
* make relationship in model
* make it HasMany relationship.
```
Repeater::make('qualifications')
    ->relationship()
    ->schema([
        // ...
    ])
```
* add validation
```
->minItems(2)
->maxItems(5)
```





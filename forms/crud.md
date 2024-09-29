* sing the mutateFormDataBeforeCreate method in Filament to modify form data before saving. In Filament, 
* the logic for manipulating data before creation or update is typically handled inside this method, 
* as you can't directly write logic in the controller like in a regular Laravel MVC structure.
```
protected function mutateFormDataBeforeCreate(array $data): array
{
    // Automatically assign the authenticated user's ID to the 'user_id' field
    $data['user_id'] = auth()->id();
    
    // Perform any other necessary data manipulation before creation
    // For example, setting a default value, formatting data, etc.
    // $data['some_field'] = 'default_value';

    return $data;
}

```
* Customizing redirects
```
protected function getRedirectUrl(): string
{
    return $this->getResource()::getUrl('index');
}
```

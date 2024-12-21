* install notifications 
```
composer require filament/notifications:"^3.2" -W
```
* must be use notifications in database in laravel , it work in filament live 

```
php artisan make:notifications-table
```
* send notifications 

```
public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->databaseNotifications();
}
```

* handled send to notification 

* I prefer that way
```
https://laravel.com/docs/11.x/eloquent#defining-observers
```
* create observed and work queue 
* steps and logic 

```
php artisan make:observer UserObserver --model=User
```
* use it in model 

```
#[ObservedBy(UserObserver::class)]
```
* handled logic 

```
public function updated(User $user)
 if() // write condition 
        {
           // logic
            if($user)
            {
                 Notification::make()
                ->icon('heroicon-o-information-circle')
                ->title(__('admin.warning'))
                ->body(__(''))
                ->actions([
                    Action::make('view')
                        ->label(__(''))
                        ->button()
                        ->url(url('admin/users/' . $user->id)),
                ])
                ->sendToDatabase($user);
            }
        }
```

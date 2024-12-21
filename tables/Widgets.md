
* First Step

```
php artisan make:filament-resource User --simple
php artisan make:filament-widget UserOverview --resource=UserResource --stats-overview
```

* Seconed Step in Resource
```
use App\Filament\Resources\UserResource\Widgets\UserOverview;
public static function getWidgets(): array
{
    return [
        UserOverview::class,
    ];
}
``` 

* The third step (charts)
```
class UserOverview extends BaseWidget
{
    protected static ?string $pollingInterval = null;
 
    protected function getCards(): array
    {
        $usersCount = User::selectRaw('
            COUNT(*) as total,
            SUM(CASE WHEN is_admin THEN 1 ELSE 0 END) AS admin,
            SUM(CASE WHEN is_active THEN 1 ELSE 0 END) AS active
        ')->first();
 
        return [
            Card::make('Total', $usersCount->total)
                ->color('primary')
                ->description('Total users'),
 
            Card::make('Admin', $usersCount->admin)
                ->color('danger')
                ->description('Admin users'),
 
            Card::make('Active', $usersCount->active)
                ->color('success')
                ->description('Active users'),
        ];
    }
}

```

__________________________________________________________________

* How to Refresh Widgets When Table Actions Are Fired

* add this steps 

* in widgets page 
```
protected $listeners = ['updateUserOverview' => '$refresh'];
``` 

* in page

```
public function updated($name)
{
    if (Str::of($name)->contains(['mountedTableAction', 'mountedTableBulkAction'])) {
        $this->emit('updateUserOverview');
    }
}
```




 



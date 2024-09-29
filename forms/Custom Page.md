# Custom Page 
* if you need write code or create pages special hard logic out resource you can make a suctom page such :- print screen ...
* **Steps**

* **step1**:
* create Filamnet Provider to register custom page
```
 php artisan make:provider FilamentServiceProvider
```
* **step2**
```
php artisan make:filament-page SortUsers --resource=UserResource --type=custom  //user resource it resource create in custom page
// sortusers name page custom
```
* **step3**
* if create any page custom must call route in same resource even if you don't use it
* you can call it in table or header create such :
```
class CreateServicesBill extends CreateRecord
{
    protected static string $resource = UserResource::class;

    protected function getHeaderActions(): array
    {
        return [
            Actions\CreateAction::make(),

            Actions\Action::make('openLink')
            ->label('')
            ->icon('')
            ->label(__(''))

            ->color('primary')
             ->url(UserResource::getUrl('route', ['activeTab' ]))

        ];
    }
}
```

* **step4**
* route call
```
 'print' => Pages\PrintFatoura::route('/print'),
```
* action button in table same resource in table

```
   ->actions([
                Tables\Actions\EditAction::make(),
             // Custom Page  Print Material Payment Sold Out
             Action::make('openLink')
             ->label('  ')
             ->icon('heroicon-o-printer')
             ->color(' ')
             ->url(fn (Model $record): string => static::getUrl('single', ['id' => $record->id]))
         
             ])
```

* UserResource --> Resource include page custom 
* **notes**
* use to make forms 
* use InteractsWithForms;
* use InteractsWithActions;

  
* **Functions**
* to translated title 
```
  public function getTitle(): string | Htmlable{
        return __('pages.retrieval_materials');
}
```
* **mount** method is responsible for resolving the record based on the URL or passed parameter, allowing you to access it throughout the class. The record can be accessed via $this->getRecord(), making it easy to manipulate or reference in your views.
  
* Here’s an example of the mount method implementation:
```
public function mount(int | string $record): void
{
    // Resolve the record from the provided ID or slug
    $this->record = $this->resolveRecord($record);
    
    // Alternatively, fetch a specific parameter (e.g., 'id') from the request URL
    $recordId = request()->query('id');

    // Pass the resolved record ID to another function, such as filling the form with the 'material_bill_id'
    $this->form->fill([
        'material_bill_id' => $recordId,
    ]);
}

```
 
* Form
```
public function form(Form $form): Form{
// input text in form
   // TextInput::make('total_price')
        //     ->label(__('form.name'))
        //     ->reactive()
        //     ->live()
        
}
```
* **submit**
```
 public function submit(){
to submit or forms such function store in mvc 
}

``` 
* **getViewData**
* to pass data to page 
```
protected function getViewData(): array
{
    // Fetch any required data to pass to the view
    $exampleData = ExampleModel::all();
    
    // Return the data as an array, similar to how you would with compact() in MVC
    return [
        'exampleData' => $exampleData,
        'additionalData' => 'Some other data', // Add any other necessary data
    ];
}

```
* **Paper form in blade**
* call form and create button only
* input make in in function create in custom page 
```
<x-filament-panels::page>

<x-filament::section>
    <form wire:submit.prevent="submit">
        {{ $this->form }}

        <div class="flex justify-center py-4">
            <x-filament::button type="submit">
                Save
            </x-filament::button>
        </div>

    </form>
</x-filament::section>


</x-filament-panels::page>
```

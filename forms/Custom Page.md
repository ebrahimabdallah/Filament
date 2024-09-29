# Custom Page 
* if you need write code or create pages special hard logic out resource you can make a suctom page such :- print screen ...

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

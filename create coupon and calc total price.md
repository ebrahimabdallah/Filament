```
// Price input with calculation logic
                             Forms\Components\TextInput::make('price')
                                 ->required()
                                 ->numeric()
                                 ->maxLength(12)
                                 ->label(__('pages.price'))
                                 ->reactive()
                                 ->validationMessages([
                                     'required' => __('validation.required'),
                                 ]),
 
                             // Discount input with reactive calculation
                             Forms\Components\TextInput::make('discount')
                                 ->numeric()
                                 ->label(__('pages.discount'))
                                 ->default(null)
                                 ->prefix('%')
                                 ->reactive()
                                 ->required()
                                 ->maxLength(2)
                                 ->validationMessages([
                                     'required' => __('validation.required'),
                                 ])
                                 ->afterStateUpdated(function ($get, $set) {
                                     $price = $get('price');
                                     $discount = $get('discount') ?? 0;
 
                                     // Calculate final price
                                     $finalPrice = $price - (($discount / 100) * $price);
                                     $set('final_price', round($finalPrice, 2));  
                                 }),
 
                             // Final Price readOnly  
                             Forms\Components\TextInput::make('final_price')
                                 ->label(__('pages.final_price'))
                                 ->readOnly()
                                 ->reactive()
                                 ->validationMessages([
                                     'required' => __('validation.required'),
                                 ]),

  ```

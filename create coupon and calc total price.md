  * This schema defines the fields for the product's pricing information:
 * - **Price**: The base price of the product, which accepts numeric values up to 12 digits.
 * - **Discount**: Percentage discount applied to the base price, with a maximum of 2 digits.
 * - **Final Price**: A read-only field that calculates the price after the discount is applied.
```
     ->schema([
        Forms\Components\TextInput::make('price')
            ->required()
            ->numeric()
            ->maxLength(12)
            ->label(__('pages.price'))
            ->reactive()
            ->validationMessages([
                'required' => __('validation.required'),
            ]),

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

        Forms\Components\TextInput::make('final_price')
            ->label(__('pages.final_price'))
            ->readOnly()
            ->reactive()
            ->validationMessages([
                'required' => __('validation.required'),
            ]),
    ])
                    
  ```

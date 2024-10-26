
* **Link Package**

```
https://filamentphp.com/plugins/eightynine-excel-import
```

* **Steps**
* first step
* install package
* use import in List Page of Resource you
```
   \EightyNine\ExcelImport\ExcelImportAction::make()
            ->color("primary")
            ->use(ProductImport::class)
            ->validateUsing([
                'category_id' => 'integer',
     ]),
```

* **Paper a Logic code**
* First step
```
php artisan make:import MyClientImport --generate 
```
* Seconed step

```
  // write logic code but not forget handled input to multilang because package not support multilang
```
* Example code to help

```
  public function collection(Collection $collection)
    {
        foreach ($collection as $row) {
           
            
            $name = isset($row[2], $row[3]) ? [
                'ar' => $this->convertUnicodeToArabic(trim($row[2])),  
                'en' => $this->convertUnicodeToArabic(trim($row[3])),  
            ] : null;
    
           
            $slug_en = isset($name['en']) ? Product::slug($name['en']) : null;
            $slug_ar = isset($name['ar']) ? Product::slug($name['ar']) : null;
            
            $slug = [
                'ar' => trim($slug_ar),
                'en' => trim($slug_en),
            ];
            
            // Check if the slug already exists  
            $check_slug = Product::where('slug->en', $slug['en'])
                                 ->orWhere('slug->ar', $slug['ar'])
                                 ->first();  
            
            // If the slug exists, append a random number to the slug
            if ($check_slug) {
                $slug['en'] = $slug['en'] . rand(100, 999);
                $slug['ar'] = $slug['ar'] . rand(100, 999);
            }
            
            $description = isset($row[4], $row[5]) ? [
                'ar' => $this->convertUnicodeToArabic(trim($row[5])),  
                'en' => $this->convertUnicodeToArabic(trim($row[4])),  
            ] : null;
    

            
            $data = [
                'name'        => $name,  
                'description' => $description,  
                'slug'        => $slug,               
            ];
    
   
            if ($name && $description) {
                Product::create($data);
            }
        }
    }
    
     public function convertUnicodeToArabic(string $string): ?string
     {
        return !is_string($string) ? null : json_decode('"' . addslashes($string) . '"'); 
     }
    
```

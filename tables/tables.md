* isToggledHiddenByDefault

* **image explaine case**
![Screenshot 2024-09-25 092758](https://github.com/user-attachments/assets/9be67497-5288-4842-80e6-e2cda75f319e)

```
 ->toggleable(isToggledHiddenByDefault: true),
```
* actions

  ```

  ->action(function (array $data, $record) {
                          
                            if ($user) {
                                 
                              //logic
                                ]);
                
                                Notification::make()
                                    ->title('Success')
                                    ->body(__('pages.add_plan'))
                                    ->success()
                                    ->send();
                            } else {
                                Notification::make()
                                    ->title('Error')
                                    ->body(__('pages.faild_plan'))
                                    ->danger()
                                    ->send();
                            }
                        })
  ```

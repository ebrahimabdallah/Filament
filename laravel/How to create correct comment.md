* We write the code with comments because we do not write it for ourselves only, and if it is only for ourselves, forgetting is quick

* Comment form on one of my codes
* first :- Write a description and summary what function to do 
* information developer write it code and date 
* write desc to response return 
* option :- add form on endpoint in postman 
* param and return function 
```
/**
     * Retrieve a paginated list of products with related currency items and images.
     * 
     * Created by : Ebrahim Reda  
     * Created at Date : 12-oct-2024
     * Edit By :Ebrahim Reda 
     * Edit at Date : 13-oct-2024  
     * 
     * This method fetches products from the database, formats the data according to the specified currency, 
     * and returns a paginated response. If no products are found, it returns a success message indicating that 
     * the products are empty.
  
     * ### URL Endpoint:
     * - GET: `/api/products`
     *
     * add Accept-currancy in header defualt it IQD 
     *
     * Note: Product currency calculations are based on manual input, 
     * not using a live API for real-time exchange rates.
     * 
     * ### Response Examples:
     * - **200 OK** (with product data):
    
    * @param  \Illuminate\Http\Request  $request  The current HTTP request instance, potentially containing a currency parameter.
    * @return \Illuminate\Http\JsonResponse  The JSON response containing the status, message, product data, and pagination information.
 */

```

* **Thans Eng:Amr Allam** 

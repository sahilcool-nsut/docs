# Backend
## Routes and Functions used
### Routes
The following routes can be found in the app.py file: 
* **/**
> 
> Just returns a welcome message to check if everything is working fine


* **/productRecommendation [GET]**
>
> Input Query: userId (int) 
>
> Returns a list of recommendations of products for a specific User ID.
>
> Example call: 
> ```
> https//:127.0.0.1:5000/productRecommendation?> userId=5
> ```

* **/getProductList [GET]**
>
> Returns the entire list of products present in the dataset products.csv.
>
> Example call: 
> ```
> https//:127.0.0.1:5000/getProductList
> ```

* **/getUserOrderHistory [GET]**
>
> Input Query: userId (int) 
>
> Returns the order history of the specified userId present in the dataset orderHistory.csv.
>
> Example call: 
> ```
> https//:127.0.0.1:5000/getUserOrderHistory?userId=5
> ```

* **/getUserBrowseHistory [GET]**
>
> Input Query: userId (int) 
>
> Returns the browse history of the specified userId present in the dataset browseHistory.csv.
>
> Example call: 
> ```
> https//:127.0.0.1:5000/getUserBrowseHistory?userId=5
> ```


### Functions
The following functions are used in the Recommender class present in Recommender.py: 

* **init()**
>
> **Parameters:** None 
>
> **Returns:** Nothing
> 
> Constructor of the Recommender() Object. 
> Initializes various variables used further in processing and computation.

* **get_orderDetails()**
>
> **Parameters:** None 
>
> **Returns:** Dataframe orderDetails
> 
> Returns the order history from the orderHistory.csv dataset 

* **get_browserHistory()**
>
> **Parameters:** None 
>
> **Returns:** Dataframe browserHistory
> 
> Returns the browse history from the browseHistory.csv dataset 

* **get_products()**
>
> **Parameters:** None 
>
> **Returns:** Dataframe products, List productsList, Int numOfProducts
> 
> Retrieves the products information from the dataset products.csv, and also returns it as a list and its count.

* **get_correlationData()**
>
> **Parameters:** None 
>
> **Returns:** Dataframe correlationData
> 
> Retrieves the precomputed data from correlationData.csv. This is further used in creating the Correlation Matrix.

* **get_correlationData()**
>
> **Parameters:** None 
>
> **Returns:** Dataframe correlationData
> 
> Retrieves the precomputed data from correlationData.csv. This is further used in creating the Correlation Matrix.

* **getDateWeights()**
>
> **Parameters:** userId 
>
> **Returns:** List of weights of the "date" attribute for that user
> 
> This function takes a User ID as input, and calculates the weights of the "date" attribute. This is done by first calculating the most recent and the last date of the user's orders, and then by standardizing the differences of all these dates.

* **getBrandDataWeights()**
>
> **Parameters:** userId 
>
> **Returns:** List of weights of the "userBrandPreference" attribute for that user
> 
> This function takes a User ID as input, and calculates the weights of the "userBrandPreference" attribute. This is done by using the previous order history of the user. All products of the brands the user had previously ordered are given a weight of boolean 1, while the rest are given a boolean 0.

* **getProductRecommendation()**
>
> **Parameters:** userId 
>
> **Returns:** List of products
> 
> This is the main function being used to get the recommendations of a user. 
> It first gets the correlation matrix for the specific user using getCorrelationMatrix() function. 
> Then, a search is made in the productsList using fuzzy logic depending upon the user's browse history. 
> After a list of potential products is found, the correlation matrix is used to finalise the final recommendations for the user.

* **getCorrelationMatrix()**
>
> **Parameters:** userId 
>
> **Returns:** 2-D Correlation Matrix
> 
> This function uses all the data of the attributes, the precomputed data and the data for a specific user and creates a Product X Product correlation matrix.

* **getUserOrderHistory()**
>
> **Parameters:** userId 
>
> **Returns:** DataFrame orderHistory
> 
> Returns the order history of the specific userId passed as the parameter

* **getUserBrowseHistory()**
>
> **Parameters:** userId 
>
> **Returns:** DataFrame browseHistory
> 
> Returns the browse history of the specific userId passed as the parameter
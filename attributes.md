## Attributes
All the numeric attributes used were standardized in a range of 0-1, so that none of the attribute dominates over others. Apart from that boolean values were also used.

### Pre Computed Attributes
#### **Price Attribute**
* The products.csv dataset has the information related to all the products, including their prices. 
* The intution behind why we are using the price as a relation attribute, is that in real life scenarios, if a user is buying products in a specific price range, there is a high chance he would keep buying items from similar price ranges.
* So, a precomputation was done regarding the standardization of the price in the range of 0-1. The formula used is: 
>  standardized_price = (maxPrice - product_price)/(maxPrice - minPrice) 

#### **Name of the Product Attribute**
* This attribute basically relates the products with each other depending on the similarity in their names. 
* For this, we used a random string, and calculated the Levenshtein Distance of each product name with this random string. Now, if there are two products with similar brands, they would be giving a similar value, and thus would be deemed as related.
* So, a precomputation was done regarding the standardization of the similarity in the range of 0-1. The formula used is: 
>  standardized_name = (maxSimilarity - product_similarity)/(maxSimilarity - minSimilarity) 

#### **Brand of the Product Attribute**
* This attribute basically relates the products with each other depending on the similarity in their brands. 
* For this, we used a random string, and calculated the Levenshtein Distance of each product Brand with this random string. Now, if there are two products with similar brands, they would be giving a similar value, and thus would be deemed as related.
* So, a precomputation was done regarding the standardization of the similarity in the range of 0-1. The formula used is: 
>  standardized_brand = (maxSimilarity - product_similarity)/(maxSimilarity - minSimilarity) 

### User Specific Attributes
#### **Brand Preference of User Attribute**
* The orderHistory.csv dataset has the information related to all the previous orders of different users. We fetch the data for a specific userId using a simple API call to our backend.
* This attribute is a very important one in deciding the recommendations, as the user would obviously love to be recommended of items of brands which he has previously ordered, considering a specific trust he has on that brand. 
* For using this attribute, first of all, we extract all the brands bought by a user in his order history, and store them in a **set**. Now, we mark all the products of that brand a boolean 1, and rest of the products a boolean 0.
* This automatically is standardized in the desired range, and also is powerful enough to affect the recommendations.


#### **Date of products ordered in previous orders Attribute**
* The orderHistory.csv dataset has the information related to all the previous order histories of different users. We fetch the data for a specific userId using a simple API call to our backend.
* The intution behind why we are using the price as a relation attribute, is that in real life scenarios, especially in grocery related shopping experiences, there is an increased tendency for repetitve orders. Thus, we gave a certain weight to previous orders of the user according to the date they were ordered on, the most recent one being given the highest.
* We calculated the difference of dates with respect to the most recent order of the user. So, if order 1 is the most recent order, it would be given a weight of 1, and the rest of the differences are calculated w.r.t this date. These are then standardized into the range of 0-1 using the same standardization formulas used above
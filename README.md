# Store_Sales

Problem statement : Nowadays, shopping malls and Big Marts keep track of individual item sales data in order to forecast future client demand and adjust inventory management. In a data warehouse, these data stores hold a significant amount of consumer information and particular item details. By mining the data store from the data warehouse, more anomalies and common patterns can be discovered.

Linear Regression model is perfect fit to analyse the data set. Because the data set value is a continous type.

Approach:
Data is loaded into the juypter notebook
Understanding of the Data: This data is related to the sales of the item in the Store 
The Variables are included in the data:Item_Identifier: Unique product ID2
      Item_Weight: Weight of product
      Item_Fat_Content: Whether the product is low fat or not
      Item_Visibility: The % of total display area of all products in a store allocated to theparticular product
      Item_Type: The category to which the product belongs
      Item_MRP: Maximum Retail Price (list price) of the product
      Outlet_Identifier: Unique store ID
      Outlet_Establishment_Year: The year in which store was established
      Outlet_Size: The size of the store in terms of ground area covered
      Outlet_Location_Type: The type of city in which the store is located
      Outlet_Type: Whether the outlet is just a grocery store or some sort of supermarket
      Item_Outlet_Sales: Sales of the product in the particulat store..


Here we need to analyse the data and need to compare the each variable with variable Item_Outlet_Sales.

 Data Cleaning : Here i found two null value containing columns. 1. Item_weight and 2.) Oulet Size here i have filled the NA values of the Item_Weight wiht the mean of the Item_Weight column. replaced Outlet_type with the mode value of the Outlet_Size column.

 Data Standardization : In Data standardization , in Item_Fat_Content there we extra set valus which were defining the same value. Therefore i have relace 'LF' with 'Low Fat'  , 'reg' with 'Regular' and 'low fat' with ' Low Fat' . I have Created extra column called New_Item_Type where i extracted the values from the  Iteem_Identifier where i have derived the first two charachter of the string which denotes the  values such as FD , DR , NC. After extracting the values to the New_Item_type i have given the fullform to the abbrevations such as FD as food , NC as non-consumable and Dr as Drinks. 
 i have then made some changes in the New_Item_type such that here we can compare the 'New_item_type' column with the non-consumable where␣ it creates the boolean value if the New_Item_type has the non_consumbale␣ value it will return as true else flase   It sets the 'Item_Fat_Content' column to the value 'Non-Edible' for all the␣ rows that satisfy the condition mentioned in the first part. In other words,␣
 for all rows where 'New_Item_Type' is 'Non-Consumable', the␣'Item_Fat_Content' column will be updated to 'Non-Edible'.

Data visualization : countplot of the Outlet_establishment_year shows that the most of the stores where opened in 1985 ans then there is the constant pace going. 
                    The density of the Item_visibility shows that the chart is skewed to the left where the maxima lies in the 0.05 .
                    BY plotting the pair plot we can observe that the Item_Outlet_Sales are affected by the Item_MRP  where the high Mrp item is being sold more often as vice versa.

Data visualization for categorical data: 
countplot shows that in Item_Fat_Content column we have more number of Low Fat items than that of the Regular Items.
when comparing with outlet sales we can observe that sales of that both Item type are the same and comparing with the MRP also the MRP for the both Item are the Same.

Plotting box plot for the item_type and item mrp show the similar trend through out as well as for the outlet sales.
plotting count plot shows that fruits and vegetables and the Snack food in most number.

Plotting count plot for the Outlet_type shows that Supermarket Type 2 are in more number compared to the other Outlet types. Other Outlet types are in the same number.
plotting box plot of Outlet size and Outlet_sales shows that  Even though Supermarket_type 1 has the highest amount of stores but the sales generated are the same when compared to the other Supermarket type. Here the Supermarket type
2 has performed well in the Outlet as compared to the other supermarket types even toh the supermarket type is low in number.

plotted a heatmap for the correlation of the variables with each other. THe Heat map shows there is relation between Item_mrp and Item_outlet sale.

Using Label Encoder i have coverted the Categorical Data type to the Numeric type for the further analysis of the model.

Modelling: splitting the data in 80 : 20 ratio as train and test.For scaling MinMax Scaling is used such that the rest all data is being standardized for  the further analysis.
Divided Train data set into X_train and y_train.
 Ran RFE for the feature seclection out of 25 best 15 features where selected.
 by using the OLS model R anda adj R values is obtained. then the manual feature elimination is done the minimize the p value of the features and VIF score. 
 After recrussive elimination of the features , final 6 features are obtained with R-valuee of 56.7 and an  adjusted value of 55 

After completing the modelling on the train data set. Modelling on the test data set is done 
The columns are dropped in the test data set to match with the train data set and then the dataset is transformed according to the train data set. After running the OLS model, we get the R2_score of 54 which is close to the R2_score of the train data set which implies that the model on the test data set is performing as per the train data set.
 
 
 Following are the columns which contribute to the Sal.
 Item_MRP', 'Item_Fat_Content_1', 'Outlet_Type_0', 'Outlet_Type_1', 'Outlet_Type_3'


By the following analysis and the linearRegression plotting we can predict the sales variable with
the following equation 
Outlet_Sales=977.55 × Item_MRP + 83.68 × Item_Fat_Content_2 - 1615.65 × Outlet_Type_0 + 349.93 Outlet_Type_1 + 1737.29 × Outlet_Type_3

 

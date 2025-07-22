California Houses Price Prediction

This project focuses on predicting housing prices in California using machine learning techniques. The dataset used for this project is the California Housing Data, which can be found [here](https://www.kaggle.com/datasets/dhirajnirne/california-housing-data).

Overview
This project demonstrates the use of four different Regression Technique to predict the housing prices - Linear, Ridge, Random forest and Gradient Boosting Regression


Summary

Following steps taken to carry out project:

STEP1: Loading the given data and Treating the Nan values with the median value
-  There were 207 Nans in the column Bedrooms which were imputed with the median value


STEP2: Drawing the facts from available data using the graphical visualization
-  From Graphical visualization we concluded that majority of the population happens to be along the ocean's coast which is followed by the middle part (Inland) of the California state
-  We also concluded that close to the ocean's cost (i.e. <1H OCEAN), median housing value tend to be higher and vice-a-versa


STEP3: Data Transformation
-  Here we had first found the correlation between the different attributes
-  We created three new attributes from the existing attributes: i) totalrooms_per_hhold = total_rooms/households ii) sparerooms_per_hhold = (total_rooms-total_bedrooms)/households     	iii) pop_per_hhold = population/households
-  We removed the attributes sparerooms, total_rooms, households, population and total_bedrooms as we have new attributes derieved from them
-  We also dropped the attributes lattitude and longitude as we donot have idea about the cities derieved from them and we like to reduce the non-linearity incurring from these 	attributes in out linear regression model


STEP4: Splitting the Transformed data randomly into Train and Test set and Performing Linear regression
-  Here we did the random split using train_test_split from sklearn.model_selection


STEP5: Standardizing data - Encoding the Categorical attribute "Oceans proximity" and Scaling the numerical attributes using the Column Transformer
-  For encoding we used OneHotEncoder from sklearn.preprocessing
-  For Scaling we used StandardScaler from sklearn.preprocessing
-  Before encoding we found the there were only five "ISLAND" values in Oceans proximity columns and so becuase of its extremely small percentage we deemed this value as outlier 	and deleted these five outliers
-  We used pipeline (from sklearn.pipeline) with columntransformer (sklearn.compose) to carry out the encoding and scaling operation of Train and Test test together


STEP6: Training the model and Predicting the results using Linear Regression
- We trained the data using linear regression and predicted the results from the Trained model
- We got the Root Mean Squared Error and R-squared value of 72035 and 0.61 repectively which were not sattisfactorily figures


STEP7: Improving the model performance: searching and removing Outliers
-  We distributed each of the given attributes into different number of bins to find the range and percentage of outliers for each attributes and removed them
-  Data is trimmed to 99 percentile for attributes median_income, totalrooms_per_hhold, pop_per_hhold and sparerooms_per_hhold in order to remove the tail outliers
-  Assuming median_income direcly proportional to median house value, totalrooms_per_hhold and sparerooms_per_hhold, we looked for the unrealistic/unlikely combination of input and 	target variables because such combination results in lower model accuracy
-  We found 32 different unrealistic/unlikely combination of input and target variables that can affect the model accuracy and with these combinations we removed 2278 rows/outliers 	in the data which is appx. 5% of the total data
-  Result after removing outliers: the correlation coefficient of i) median_income w.r.t median_house value is increased from 0.689 to 0.747 ii) sparerooms_per_hhold w.r.t 	median_house value is increased from 0.191 to 0.470 iii) totalrooms_per_hhold w.r.t median_house value is increased from 0.152 to 0.461 iv) housing_median_age w.r.t 	median_house value is slightly decreased from 0.105 to 0.076 v) pop_per_hhold w.r.t median_house value is decreased from -0.024 to -0.257
-  Above results show that the unrealistic/unlikely combination of input and target variables which we chosen has really helped to improve the oveall correlation of input attribute 	with the target attribute


STEP8: Improving the model performance: Stratified splitting of Train and Test set to avoid sampling bias
-  Used StratifiedShuffleSplit from sklearn.model_selection for splitting into train and Test data
-  StratifiedShuffleSplit was carried out on the basis of Income category
-  Created a new column called "Income_cat" based on the following income band:
-  Income between 1-1.5 is named as Category-1
-  Income between 1.5-3.0 is named as Category-2
-  Income between 3-4.5 is named as Category-3
-  Income between 4.5-6.0 is named as Category-4
-  Income above 6 is named as Category-5
-  StratifiedShuffleSplit ensures the data is split equally from each income category to avoid the sampling bias between Train and Test data
-  After StratifiedShuffleSplit, the column "Income_cat" is deleted


STEP9: Standardizing the data and performing Linear regression
-  Again used OneHotEncoder and StandardScaler from sklearn.preprocessing for encoding the categorical column and scaling the numnerical columns of input attributes
-  Linear regression is performed to train the data and then the train model is used to predict the test data
-  Result from Linear regression:
	Root Mean Squared Error for test model is now improved from 72035 to 60485
	R-squared for test model is now improved from 0.610 to 0.698
-  There is a significant improvement in the accuracy of model with the removal of outliers and then stratified splitting the Train and Test data


STEP10: Comparison of different Regression models- Linear, Ridge, Random forest and Gradient Boosting Regression
-  Carried out all the four regressions (Linear, Ridge, Random forest and Gradient Boosting Regression) in one operation to compare the results from them
-  The results from linear and Ridge regression fetched almost same results:
-  Linear Regression result: RMSE: 60485.79 R^2 score: 0.70
-  Ridge Regression result: RMSE: 60482.67 R^2 score: 0.70
-  The results from Random Forest and Gradient Boosting regression fetched almost same results abd are far better than Linear regression results:
-  Random Forest Regression RMSE: 53949.07 R^2 score: 0.76
-  Gradient Boosting Regression: RMSE: 54219.11 R^2 score: 0.76
-  The above results show that Random Forest Regression is the best regression model with RMSE of 53949.07 and R-squared value of 0.76


STEP11: Linear regression with one independent variable - median_income
- Result from this regression:
	Root Mean Squared Error for test model: 72106
	R-squared for test model: 0.571
- Conclusion: Linear regression with one independent variable median_income is proved to be bad model than our model with the transformed and standardised model with stratified 	splitting between Train and Test set. The difference in performance parameters is huge
- It is to be noted that this model does not include parameters like longitude and lattitude. Also this model doesnot include the "ISLAND" value in the categorical column "oceans 	proximity". These are the limitations of this model
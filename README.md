# Assignment Name: Boom bikes 
	
Problem Statement
A bike-sharing system is a service in which bikes are made available for shared use to individuals on a short term basis for a price or free. Many bike share systems allow people to borrow a bike from a "dock" which is usually computer-controlled wherein the user enters the payment information, and the system unlocks it. This bike can then be returned to another dock belonging to the same system.


A US bike-sharing provider BoomBikes has recently suffered considerable dips in their revenues due to the ongoing Corona pandemic. The company is finding it very difficult to sustain in the current market scenario. So, it has decided to come up with a mindful business plan to be able to accelerate its revenue as soon as the ongoing lockdown comes to an end, and the economy restores to a healthy state. 


In such an attempt, BoomBikes aspires to understand the demand for shared bikes among the people after this ongoing quarantine situation ends across the nation due to Covid-19. They have planned this to prepare themselves to cater to the people's needs once the situation gets better all around and stand out from other service providers and make huge profits.

They have contracted a consulting company to understand the factors on which the demand for these shared bikes depends. Specifically, they want to understand the factors affecting the demand for these shared bikes in the American market. The company wants to know:

   1. Which variables are significant in predicting the demand for shared bikes.
   2. How well those variables describe the bike demands.


Business Goal:
You are required to model the demand for shared bikes with the available independent variables. It will be used by the management to understand how exactly the demands vary with different features. They can accordingly manipulate the business strategy to meet the demand levels and meet the customer's expectations. Further, the model will be a good way for management to understand the demand dynamics of a new market. 

## Table of Contents

## General Information
  The business goal is to model the demans for shared bikes with the available independent variables. It is used by the management to understand how the demand vary with diferent features. Based on this business can manipulate the business strategy to meet the demand levels.
  
  Followed the below steps to design the model.
  
  1. Data Understanding: There are 730 rows and 16 columns provided in the bike.csv file. 
	 It contains about the applicants information how many bikes rented on specific date ,weather, season, temperature, holiday, weekday etc.
	 
  2. Data Cleaning & Manipulation:
	a.Fixed the rows and columns: 
		There are no null values in the data.
		
	b. Data Transformation:
	   Converted the Season, Mnth, weatherist and weekday to the respective categorical vaariables to analyse the data.
	   		
  3. Univariate Analysis: First we identify the numerical, categorical and other typs of data.
     a. Drawn the pair plot and pie chart for numerical variables.
		Observation from above plots.
		1. There is a strong correlation between cnt and temp, atemp, hum and windspeed.
	 b. Drawn the box plot to identify the outliers.
	
	Below observations from the above graphs.
		 - People are renting more times bikes during summer and fall season.
		 - Bike renting are more September and October month.
		 - More bikes are rented in Clear weather condition.
		 - Saturday, Wednesday and Thursdays are more bikes rented.
		 - There is not much difference in the count for the working day or not.
		 - Bike rentals are more in Holidays time.
		 - Bike rentals are increased in year 2019.
					
 4. Bivariate Analysis:
   Drawn the box plot between season, cnt and weekday. 
   Below Observation from the Bivariate analysis:

    - During Summer Season - Sat, Thu and fridays are more bike rented.
    - During Fall Season - Wed, Thu and fridays are more bikes rented.
5. Created dummy variables for Catagirical variables(Season, mnth, weekday and weatherist.

6. Splitting the Data into Training and Testing Sets. Used the MinMaxScaler rescaling features.
	- Draw the heatmap to find the coorreltion between variables.
	- based on the heat map we see the 'cnt' is most correlated with 'temp' and 'atemp'. Let's see a pairplot for `cnt vs `atemp`.
7. Building a linear model
   Fit a regression line through the training data using `statsmodels`. Remember that in `statsmodels`, you need to explicitly fit a constant using `sm.add_constant(X)` because if we don't perform this step, `statsmodels` fits a regression line passing through the origin, by default.
   - Build the linear model by adding all the variables to the model.
   - By observing the p-vaues 
   - Looking at the p-values, it looks like some of the variables aren't really significant (in the presence of other variables).
   - We could simply drop the variable with the highest, non-significant p value. A better way would be to supplement this with the VIF information.
   - Checking VIF: Variance Inflation Factor or VIF, gives a basic quantitative idea about how much the feature variables are correlated with each other. It is an extremely important parameter to test our linear model
    - R-Squared is 0.851, which means 85% of the variance of the 'Cnt' is explained by all the variables.
	- We will use the Recursive Feature Elimination(RFE) Automated Approach to drop the variables. This is the optimal feature selection.
8. Building a Model with selected columns using the RFE approah.
    - Validate the mode using the VIF values.
	- Dropping the variable and updating the model:
		below approach followed:

		- High p-value, high VIF : definitely drop
		- High-Low:

			 1) High p, low VIF : remove these first, then build model again and check VIF again      
			 2) Low p, high VIF : remove these later          
		- Low p-value, low VIF : keep variables
	
9.  Dropping the next Variable and updating the Model until we get the VIF value < 5 and p-value is < 0.05	
10. Residual Analysis of the train data: Below points are analysed to decide the model is best fit or not:

	The model p-value, the VIF and the R-squared value. 
	The p-value gives us input on the significance of the variables, the VIF about the correaltion between the participating variables and the R-squared value gives us an indication about the strength of the model. 

	1. The low p-vaue or p <0.05 of the selected variables. 
	2. The VIF value should be <5 . We achieved the both parameters in the above model.
	3. The R-squared value is 83.6% , which tells the high correlation between the dependent variable (cnt) and the independent variables.
	   The selected variables helps us to map the variance of the dependent variables 'cnt'
11. Making Predictions Using the Final Model
    Now that we have fitted the model and checked the normality of error terms, it's time to go ahead and make predictions using the fina model.
12. Model Evaluation: Let's now plot the graph for actual versus predicted values.
	We can now validate the assumptions of linear regression in the model:

	As we can see, temperature has a linear relationship with the dependent variable (cnt). 
	As we have observed earlier every variable in our chosen model has a VIF < 5,  which ensures that there is no mulitcollinearity. 
	The error distribution as observed above is normal (ie concentrated around 0) which is another assumption of linear regression. 
13. Prediction and Evaluation of the test set using r2_score
	r2 score on the test set is 0.8179669424739718
	r2 score on the train set is 0.8359991965394293

  We can see that the equation of our best fitted line is:

   cnt = 0.236 * yr -0.088 0.202 * holiday + 0.412 * temp - 0.142 * windspeed -0.11 *spring + 0.058 * winter - 0.053 * Dec - 0.056 * Jan - 0.06 *July - 0.05* Nov + 0.056*Sept - 0.29 * Light Snow - 0.082 * Mist+Cloudy.
   
14. Calculate the the MSE (Mean Squared Error)
   Mean squared error of the train set is 0.008256279849003385
   Mean squared error of the test set is 0.008256279849003385
   
   Our models MSE is almost 0, it implies that our model accurately predicts the variance between in both the test and train datasets.
	

## Conclusions
The summary of this model after data interpretation, visualisation, data-preparation, model building and training, residual analysis and evaluation of test model are as follows.

1. The R-squared value of the train set is 83.6% , whereas the test set has a value of 81.8%. Which suggests that our model explains the variance quite accurately on the test set and thus we can conclude that it is a best fit good model.

2. Our developed model's MSE(Mean Squared Error) is almost 0 for both the train and test datasets which suggests that the variance is accurately predicted on the test set.

3. The p-values and VIF were used to select the significant variables. RFE was also conducted for automated selection of variables.

4. We can conclude that the bike demands for the BoomBikes is company is dependent on the temperature and whether it is a workingday or not. Also the more bike rentals are demanded on the winters as compared to the summer and spring.

  We had observed that the September month had higher use of rentals. In terms of days the maximum focus was on days like Wed, Thurs and Sat and more on working day.

5. These interpretations help us derive meaningful insights in the bike rental market and the behaviour of the people.
One of the recommendations based on this model are that there should be more marketing required in the summer and spring season to drive up rentals.

Also Business has to introduce the incentives or any deals on the days the weather is less clear.

There are more Rentals in 2019 than 2018, which suggests that over time more people would be exposed to this idea and there has to a strong analysis done to retain the repeated customers.

## Technologies Used
	Python (Version 3.11.7)
	Numpy  (Version 1.26.4)
	Pandas (Version 2.1.4)
	Matplotlib (Version  3.8.0)
	Seaborn (version 0.13.2)

## Acknowledgements 
	This assignment is created based on the trainings provided by UpGrad Team.

## Contact
  Created by Kushalava Reddy Yanala   
  GitUsernames (@ykreddy321 )

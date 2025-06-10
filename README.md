# Project 4 Home Sales

Google Slides Deck: https://docs.google.com/presentation/d/17sejluZsZA4_xemRHWpfLncSm06TlfVYHXxHatSkIO4/edit?slide=id.g41a8f1e756_0_702#slide=id.g41a8f1e756_0_702

## Project Team
 - Nicolette Sorensen
 - Deborah Kisch
 - Janice Guallpa
 - Kelley Blue
 - Jennifer Robison

## Project Overview
Project 4 pulls together skills learned throughout the Data Analytics Bootcamp to create a Real estate map and prediction model. An interactive map shows real estate sales in the target area. A web interface allows users to input the number of bedrooms, bathrooms, and size of house and lot. An html-based interface is connected to a machine-learning model. The model uses Random Forest to predict the optimal sale price for the house. 

## Data Source
 - Used API for realtor.com to call for single family homes in/around St. Paul, MM.
 - Used Pandas to pull desired data: list price, list date, sold price, sold date, bedrooms, baths, square footage, lot square footage, address and coordinates.
 - Formatted dataframe and save as a .csv file.

## Predicting Home Sales and Market Duration in Saint Paul
Analyzed home sale data in Saint Paul, Minnesota to:
1. Develop and compare various regression models to find the best-performing solution to predict the sale price and estimate how long a house stays on the market.
2. Predict the sale price of a house based on features like square footage, number of beds/baths, and lot size and created a model for integration in to a site.

### 1. Model_Selction.ipynb in Model_Selection Folder
Compare multiple machine learning models to predict sold_price and days_on_market.  
Steps Taken:  
 - Upload st_paul_sold_properties.csv performed data processing and data clean-up.
 - Cleaned and engineered features (computed days_on_market).
 - Explored data using correlation heatmaps.
 - Tested 8 regression models (e.g. Random Forest, Gradient Boosting, Ridge, Lasso).
 - Evaluated performance using MAE and R2.  
Results  
 - Random Forest gave the best result for both sold price and days on market. Followed close by Gradient Boosting.
 - Predicting sale price was more accurate than days_on_market (R2 for DOM was low).

### 2. Price_Sold_Regression.ipynb in Model_Selection Folder
Optimize a single model (Gradient Boosting Regressor) to reliably predict sold price.
 - Added new features like beds_baths_ratio and lot_to_sqft_ratio.
 - Created a machine learning pipeline with preprocessing steps.
 - Perfomed hyperparameter tuning using GridSearchCV.
 - Final model saved to disk as sold_price_model.pkl.  
Result  
 - Achieved R2 of 0.828 on the test set with slight overfitting of R2 training vs test.
 
 ### 3. Days on Market model
Used XGBoost, a type of decision tree machine learning model commonly used in real estate.
Steps Taken: 
 - Loaded the .csv file into the model and performed data pre-processing
 - Calculated days on market by subtracting sold_date from list_date
 - dropped unnecessary columns: list_date, sold_date, city, street, latitude, longitude, zip, list_price, sold_price
 - Split the data into training and testing, then set up the model. 
 - Ran GridsearchCV to determine the best parameters, determined the feature importance. 
 - Re-ran the model after dropping additional column and adjusting the parameters. 
 - Many attemps were made to optimize this model, however, results peaked at 73% R2 accuracy. 
 - Ultimately, the group decided not to include this model in the final project due to the low accuracy.

## Create Folium map 
 - Create Flask call
 - Upload CSV and preprocess sold price, beds, baths, sqft, longitdue and latitude columns
 - Normalize the data with scaler
 - Create user input areas
 - Create Folium map to show recently sold homes that match a users input (beds, bath, square footage)
 - Include pop-up markers to include sold price, sqft, beds, baths, sqft

## Flask Backend: Tying it all together
### Connected the trained regression model to a Flask server, creating API endpoints that:
 - Predicts a home’s sale price based on user input (beds, baths, square feet, lot size)
 - Returns a list of the most similar homes sold, based on calculated ratios and features
 - Frontend with Interactive Map
### Designed and implemented an HTML/JavaScript interface that:
 - Lets users adjust home features with sliders
 - Instantly shows the predicted price
 - Displays a Leaflet.js map of similar homes, each with a detailed popup showing price, beds, baths, square footage, lot size, and full address
### UX Enhancements
 - Created live prediction updates as users interact with sliders
 - Implemented debouncing to limit backend calls
 - Added interactive tooltips and map markers to improve usability
### Tools & Technologies
 - Python, Flask, Pandas, NumPy, Scikit-learn
 - HTML, JavaScript, Leaflet.js
 - CSV data pipeline and joblib for model loading

## References
- This data is publicly available on Realtor.com.
- Guidance on overlaymaps, jupyter notebook tabular table, and JavaScript coding was sourced from theXpert Learning Assistant Chat+, an AI Learning tool for Edx, as well as Microsoft Copilot.  
- Used google for leaftlet maps and marker functions accessed June 2025.

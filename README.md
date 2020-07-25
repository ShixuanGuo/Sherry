# Wholesales Volume Prediction

## Part 1 Project Introduction
1. **Goal**  
By extracting data from websites and analyzing historical sales data, build a model to predict the monthly sales volume of each product.  
2. **Data**  
  - 4 years historical sales and product data for 70 products from year 2016 to year 2019: sale volume, price, rebate, promotion, discount, segment, brand, package, SKU code, region and date (YY-MM)
  - External data: temperature, holiday, etc. (Extracted from websites)  
3. **Steps**  
  - Exploratory data analysis
  - Data preprocessing
  - Feature engineering
  - Model buidling: Time series ARIMA model; Machine learning model; Combination model
4. **Packages**  
  - ProfileReport
  - Pandas
  - Numpy
  - Matplotlib
  - Datetime
  - Sklearn

## Part 2 Exploratory data analysis  
1. **Trends**  
    One important factor of time-series is trends. To identify the long-term trends, I visualzied sales volume VS month and clustered products by different features. 
    Some insights:  
    - By segment, middle-end market has downward long-term trend while high-end market has clearly upward long-term trend.  
    - After the new product launched, some products' sales volume decreased.  
    <img src="" alt="trend" width="666" height="485">
2. **Seasonality**  
    Another very important factor of time-series is seasonality which represents the repeating pattern within each year. 
    Some insights:  
    - High-end and low-end market have very similar seasonality, while middle-end market sometimes has opposite variations. 
    - Most products have peaks at the beginning of each year (Jan, Feb) and at summer of each year (Jul, Aug).   
3. **Correlation**  
    Some features might have relationship with each others. To check correlations, I calculate statistics and visualized data using `report=ProfileReport(df_data, explorative=True)`  
    Some insights:  
    - As price goes up, most products' sales volume goes down. Price has strong negative correlation with sales.  
    - Different packages have clearly different average prices. 
    - Rebate, discount and promotion have strong positive correlation with sales.  
    <img src="" alt="correlation" width="666" height="485">  
Exploring data trends, seasonalities and correlations can help us a lot when selecting features and building models.  

## Part 3 Data preprocessing
1. **Missing data**  
  Usually, there are three methods used to deal with missing values: a) using statistics, such as average value, b) using the nearest value, c) using regression. 
  In this project, most missing values are prices concentrated at year 2016. As most products only changed price few times, once in each year and only changed a little, I use the nearest value to fill missing values.  
2. **Outliers**  
  As many products have peaks at specific months and different products have very different sales volumes, it is dangerous to drop values based on its distance to the average and trend. Thus, I first pick out products whose sales volume have very high variation. Second, I visualized these products' sales volume and drop outliers that are not peaks.  
2. **Log Transform**
  By plotting the distribution of price, rebate, promotion and discount, I find they are all positive values and significantly skewed. Thus, I apply log transform: 
  `data['log'] = data['value'].transform(np.log)`  

## Part 4 Feature engineering
1. **Create new features**  
  - Create interaction features: for example, 'sales volume portion at t-i (i=1,2...12)'
  - Create dummy variables: categorical variables like brand, segment and package.  
2. **Add new features from additional resources**  
  Based on insights from EDA, I added features like temperature, holiday, number of weekends at each month. Extracted data from websites and reports.  
3. **Remove unused features**  
  I remove features which:  
  - wouldn't be available at the time of prediction
  - dosen't have enough variation or most of its values are 0
  - has too many missing values

## Part 5 Model building

## Part 6 Model optimization
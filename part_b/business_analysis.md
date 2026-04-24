### ***PART B- BUSINESS CASE ANALYSIS***





##### ***B1: PROBLEM FORMULATION***



**#B1 (A)- #UNDERSTANDING THE PROBLEM**



This can be seen as a supervised learning problem where we try to predict how many items will be sold for a given store and promotion. The main target variable here is items\_sold, since the company wants to increase the number of products sold.



The input features can include things like store size, location type, promotion type, competition density, whether it is a weekend or festival, and similar factors that may affect customer buying behaviour.



This is regression problem because the output is a number, not a category. We are trying to estimate a value rather than classify something.





**#B1 (B)- CHOICE OF TARGET VARIABLE**



Using total revenue may not always give the right idea about how well a promotion is working. Revenue can change because of a price difference or discounts, so it does not always reflect actual demand.



Items sold is a better option because it directly shows how many products customers are buying. It is a more stable way to measure the impact of a promotion.



This shows an important point in machine learning -the target variable should match what we actually want to measure. If the target is not chosen carefully, the results can be misleading.





**#B1 (C)- ALTERATIVE MODELING STRATEGY**



Using one single model for all stores might not work well because different locations behave differently. For example, people in urban areas may respond differently to offers compared to rural areas.



A better approach would be to group stores based on location and build separate models for each group. Another option is to include location-related features more carefully in the model so it can learn these differences.



This helps the model perform better because it takes into account the variation in customer behaviour across different stores.





##### ***B2: DATA AND EDA STRATEGY***



**#B2 (A)- DATA JOINING AND STRUCTURE** 



The data is coming from different tables, so first they need to be combined into a single dataset. The transaction table can act as the base since it contains the actual sales records. It can be joined with store attributes using the store\_id, and with promotion details using the promotion\_type or promotion id. The calendar table can be joined using transaction\_date.



After joining, the final dataset should have one row per transaction (or per store per day, depending on the data). This makes it easier to track how each store perform over time.



Before modelling, some aggregations can be useful. For example, total items sold per day per store, average basket size, or number and making patterns clearer for the model.





**#B2 (B)- EDA STRATEGY**



Before building a model, it is important to explore the data to understand patterns and issues.



First, I would check the distribution of items\_sold using a histogram to see if the data is skewed or has outliers. This helps decide if any transformation is needed.



Second, I would compare items sold across different promotion types using a bar plot. This shows which promotion are more effective.



Third, I would analyse trends over time using a line plot of sales by date. This helps identify seasonality or sudden changes.



Fourth, I would check relationship between numerical variables using a correlation heatmap. This helps understand which features are strongly related to sales.



These analyses help in deciding which features to keep, transform, or create before modelling.





**#B2 (C)- HANDELING IMBALANCE**



If 80% of the transaction have no promotion, the model may learn to focus mostly on non-promotion cases and ignore the effect of promotions. This can reduce its ability to correctly learn how promotions impact sales.



To handle this, we can balance the data by giving more importance to promotion records or by sampling the data more evenly. Another approach is to create features that clearly highlight promotion effects so the model can learn their impact better.





##### ***B3: MODEL EVALUATION AND DEPLOYMENT***



**#B3 (A)- TRAIN-TEST SPLIT AND EVALUATION**



Since the data is time based (monthly data over three years), the split should also follow the time order. The earlier data (for example, 2-2.5 years) can be used for training, and the most recent months can be used for testing.



A random split is not suitable here because it would mix past and future data. This can lead to unrealistic results , as the model may indirectly learn from future patterns.



For evaluation, I would use metrics like RMSE and MAE. RAMSE gives more weight to large errors, so it helps identify cases where predictions are far off. MAE gives the average error in a simple way, which is easier to interpret. In this business context, lower values of these metrics mean the model is predicting sales more accurately.





**#B3 (B)- UNDERSTANDING MODEL RECOMMENDATIONS**



If the model suggests different promotions for the same store in different months, it likely means that the features for those months are different. For example, December may have higher demand due to festivals, while March may have normal conditions.



Using feature importance, we can check which factors influenced the prediction the most. This could include things like seasonality, past sales trends, or competition.



To explain this to the marketing team, I would show that the model is not randomly changing decisions, but is adjusting based on patterns in data. For example, higher demand months may favour one type of promotion, while lower demand months may need a different strategy.





**#B3 (C)- DEPLOYMENT AND MONITORING**



After training, the model can be saved using a method like joblib or pickle. This allows the same trained model to be reused without training again every month.



At the start of each month, new data for all stores can be prepared in the same format as the training data. This data is then passed into the saved model to generate predictions or recommendations.



For monitoring, we can track model performance over time by comparing predictions with actual sales. If the error starts increasing or patterns change, it may include that the model is no longer performing well.



In the case, the model should be retrained using more recent data so that it says updated with current trends.




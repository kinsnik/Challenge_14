# Challenge_14: Machine Learning Trading Algo


**In this Challenge we created trading algorithms based on the SVM, SVC model and the Logistic Regression model.**

After tuning the algo for the SVM, SVC model by adjusting the size of the training dataset, via the DateOffset function and adjusting the SMA input features, sma_fast and sma_slow, and comparing it to the Logistic Regression model, I determined that the SVM model was more accurate but the Logistic Regression model had better recall and precision. 

Original classification report for the baseline trading algo. 

![SMA 4 and 100, 3 month training Classification Report](/Screenshots/sma4_100_3monthdateoffsetclassreport.png)

Original cumulative return plot for the baseline trading algo 

![SMA 4 and 100, 3 month training Cumulative Return Plot](/Screenshots/sma4_100_3monthdateoffsetcumulativereturns.png)


**Tuning the SVC training algorithm by adjusting the size of the training dataset**

I sliced the data into different periods, changing the training sample from 3 months to 1,6 and 12 months. It seemed like increasing the training window in this scenario marginally improved the accuracy at the cost of poorer recall. At 12 month training sample, there was 0% recall on selling short (-1) indicating the algo would not be able to predict when to sell, and would therefore incorrectly signal buys nearly 100% of the time. Decreasing the period to one month also had the same effect on recall without improving accuracy. This leads me to believe that 3 months is the "sweet spot" for our training period .

This was the 1 month Classification Report

![SMA 4 and 100, 1 month training](/Screenshots/sma4and100_1monthdateoffsetclassreport.png)

This was the 6 month Classification Report

![SMA 4 and 100, 6 month training](/Screenshots/sma4and100_6monthdateoffsetclassreport.png)

This was the 12 month Classification Report

![SMA 4 and 100, 12 month training](/Screenshots/sma4and100_12monthdateoffsetclassreport.png)


**Tuning the SVC trading algorithm by adjusting the SMA input features**

For SVC I increased the sma short window to 10 and long window to 150 and it looked like the recall for sells (-1) vastly improved (from 0.04 to 0.26) and recall of buys (1) fell (from 0.96 to 0.72). Meanwhile, precision remained about the same at the cost of a small dip in accuracy (from 0.55 to 0.52). I also then increased the short window to 50 and long window to 200, which had a similar result to increase the training window to 12 month. It seems like using larger sma windows, 50 and 200 in this case, generated only buy predictions (1) since the recall for 1 was 1.00 and accuracy was 0.56 and precision and recall for -1 was 0. 

This was the SMA_Fast = 50, and SMA_Slow = 200 and 3 month DateOffset Classification Report

![SMA 50 and 200, 3 month training Classification Report](/Screenshots/sma50and200_3monthdateoffsetclassreport.png)

This was the SMA_Fast = 10, and SMA_Slow = 150 and 3 month DateOffset Classification Report

![SMA 10 and 150, 3 month training Classification Report](/Screenshots/sma10and150_3month.png)


The set of parameters that was found to best improve the returns were sma_fast =10 and sma_slow = 150 and the training window is 3 months. 


**Logistic Regression Model**

For Logistic Regression I used the same paramters as the ideal SVC model, sma_fast = 10, sma_slow = 150 and DateOffset = 3months.  I determined that the SVM model was more accurate but the Logistic Regression model had better recall and precision. 

Logistic Regression Classification Report

![SMA 10 and 150, 3 month training Classification Report using LR](/Screenshots/sma10and150_3month_LRModel.png)

Logistic Regression Cumulative Returns Plot

![SMA 10 and 150, 3 month training Cumulative Return Plot using LR](/Screenshots/CumulativeReturns_LR.png)
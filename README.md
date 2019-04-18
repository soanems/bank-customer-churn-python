# Bank Customer Churn in Python

In this repository, I used Python to analyze bank customer churn.

On jupyter notebook, I went through the bank custumer churn data. My focus was to process the data for modelling, and try different algorithms to evaluate their performance.

First I analized the features, to try to understand them, and have some insights.

Second, I started to prepare the data for the modelling. 
  * Applied a one-hot-encoding over the cathegorical features. 
  * Splitted the data into the train and test sets
  * Standardazing the features on each set. 
 
Third, the modelling was done in two parts:
  * With the complete train data
  * With a balanced train data. 
  
For each part I test the same models and algorithms:

* Logistic Regression (Scikit-Learn)
* Multi-Layer Perceptron (Scikit-Learn)
* Gradient Boosting (Scikit-Learn)
* Extreme Gradient Boosting (XGBoost)
* Light Gradient Boosting Machine (LightGBM)

Initially, I tested the models performance on the unbalanced traning set. 

When looking to the *pure accuracy score*, they all behaved reasonably well. Only the *logistic regression* was one step behind. However, the data is imbalanced. 80% of the data are clients that didn't exited (labeled as 0). So, if we create a model that predicts 0 for all the clients, its accuracy will be of 80%. A better score metric is the *balanced accuracy*, that weights the classes by occurence. For the *balanced accuracy*, the baseline, for a binary classification, is of 50%. Looking at the *balanced accuracy* for all the predictions, the *logistic regression* did a poor job, with 59% accuracy. The other models had a balanced accuracy from 72% to 74%, with the *lightGBM* being slightly better, when also looking at the recall of the exited clients (labaled as 1).

Trying to improve the predictions for the exited clients (label 1), I proposed to *balance the train data*, by simply ramdonly removing clients labeled as 0 until the number of exited and not exited were almost the same. When I did that, I was expecting that the *accuracy* and the *balanced accuracy* to have similar values for each model, and that was exactly what happened. For all the models, the *balanced accuracy* increased to up to 79% (*LightGBM*), and showed that the *tree based classifier models* worked better.

By looking at the *score metrics and speed performance*, the model I would chose is the *Gradient Boosting Classifier* from the *LightGBM* package. But the *XGBoost* is close behind.

However, I still believe I can improve the accuracy by applying feature engineering on the data, as well trying other models, even doing an ensemble model over all the tested models.

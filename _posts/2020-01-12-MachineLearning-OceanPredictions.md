---
layout: post
title: Machine Learning for the Ocean!
subtitle: Fitting Regression models.

---
#### Choosing a target, evaluation metric, and baseline for regression:
In order to to predicit ocean water temperature, Seems like I'm starting from the end but bare with me while I go over the steps 
one would use in a busines scenario to get valuable insights and predictions to solve an issue, or improve a process by using insights
and predictions that would beat baseline. 
As a target  I choose Water Temperature from the data set provided in my previous post! As an evaluation Metric I choose Mean Absolute
Error since even though I'm dealing with a somewhat large amount of a data and variations, my target values are about 20 different values.
Whats a baseline: After identifying what you want to predict and the business problem you want to solve, try and get to a baseline
asap and try to beat it with more complex robust models and then tweek parametres to improve your predictions scores.
Train/Val/Test: Making sure to split your data right is the first step of success while avoiding leakage and selecting best features
would come as a logical next step. I cannot stress enough how important it is to keep your test data until you are satified with your model.
then test it on your test split.


#### Fitting and evaluating models
As a start in this case I used a simple linear regression since I'm dealing with ordinal values, that gave a baseline of 22% 
accurency, and that is my baseline to beat.
I switched between a onehotencoder and a targetencoder to experience with which I highly recommend then ended up settling with oridnalencoder for couple
reasons(minimizing computational power and ime)
Second I fitted a Decision Tree Regressor whith a max depth of 2 which predicted an even worse accuracy than baseline, then wiggled with it till I found the optimal depth in this situation was 10.
To get more insight on how the model did since Trees tend to overfit data, I then fitted a Random Tree Regressor with the depth of 10th which significantly improved my accuracy to 78.62%. Not bad right? I know lol
But then in the search of better predictions, I fitted couple more models which I highly recommend, Its a fun process I promise.
So I fitted Gradient Boosting Regressor and tweeked its hyperparametres till it did as good as the Random Forest, at this point I knew if I was to get better accuracy, it'll be only by a fraction. 
Then I fitted an XGboost Regressor to see and understand how the type of model was going to perform when trained on my data, still no success to beat the Random Forest and Gradient Boosting.
To validate all of this as I mentioned above I choose MEA as an evaluation metric and that when things became intersting and had best metric through the Gradient boosting model, which I choose to implement in my app to do live predicting with MAE of 1.32 degrees Celsius.
![Crepe](/img/winddirwatertempbars.png){: .center-block :}



 

### Heat maps ###
Showcasing correlation between Swell Direction & Wave Heights
![Crepe](/img/heatmapswelldirwaves.jpg){: .center-block :}
Showcasing correlation between Wind Direction & Wind Speed
![Crepe](/img/winddirwindspeed.png){: .center-block :}



The code to make a pipeline:
_(rest of code step by step will be linked in my github)_
[see code version here](https://github.com/MehdiKhiatiDS/DS-Unit-1-Build/blob/master/Project_Up_Welling!.ipynb)

```javascript
import category_encoders as ce
from sklearn.model_selection import train_test_split
from sklearn.pipeline import make_pipeline
from sklearn.tree import DecisionTreeClassifier
from sklearn.tree import DecisionTreeRegressor
from sklearn.impute import SimpleImputer
from sklearn.ensemble import RandomForestClassifier
from sklearn.ensemble import RandomForestRegressor
from sklearn.ensemble import RandomTreesEmbedding
from sklearn.ensemble import GradientBoostingRegressor
from sklearn.ensemble import VotingRegressor
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import roc_curve
from sklearn.metrics import multilabel_confusion_matrix
from sklearn.linear_model import PassiveAggressiveClassifier
from sklearn.linear_model import RidgeClassifier
from sklearn.linear_model import PassiveAggressiveRegressor
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_absolute_error
pipeline = make_pipeline(
    ce.OrdinalEncoder(), 
    SimpleImputer(strategy='median'), 
    GradientBoostingRegressor(n_estimators=1000, subsample=0.8)
)

# Fit on train, score on val

pipeline.fit(X_train, y_train)
print('Train Accuracy', pipeline.score(X_train, y_train))
print('Validation Accuracy', pipeline.score(X_val, y_val))
print('Validation Accuracy', pipeline.score(X_test, y_test))
```

_Sources_: [NOAA](https://www.ndbc.noaa.gov), [Ocean Motion](https://www.oceanmotion.org), [UCSD](https://ucsd.edu)

[_Link for step by step coding process on github:_](https://github.com/MehdiKhiatiDS/DS-Unit-1-Build/blob/master/Project_Up_Welling!.ipynb)






---
layout: post
title: Machine Learning for the Ocean!
subtitle: Fitting Regression models.

---

![Crepe](/img/tahiti.jpg){: .center-block :}

#### Choosing a target, evaluation metric, and baseline for regression:
In order to predicit ocean water temperature... seems like I'm starting from the end but bare with me while I go over the steps one would use in a business scenario to get valuable insights and predictions to solve an issue, or improve a process by using insights and predictions that would beat baseline. 
As a target  I choose Water Temperature from the data set provided in my previous post! As an evaluation Metric I choose Mean Absolute Error since I'm dealing with a large amount of data and variations, my target values are about 20 different values.
What's a baseline? After identifying what you want to predict and the business problem you want to solve, try and get to a baseline asap and try to beat it with more complex robust models and then tweek parametres to improve your predictions scores.
Train/Val/Test: Making sure to split your data right is the first step of success while avoiding leakage and selecting best features would come as a logical next step. I cannot stress enough how important it is to keep your test data until you are satisfied with your model then test it on your test split.


#### Fitting and evaluating models
As a start in this case I used a simple linear regression since I'm dealing with ordinal values, that gave a baseline of 22% 
accurency, and that is my baseline to beat.
I switched between a onehotencoder and a targetencoder to experience with which I highly recommend then ended up settling with oridnalencoder for couple reasons (minimizing computational power and time).
Second I fitted a Decision Tree Regressor with a max depth of 2 which predicted an even worse accuracy than baseline, then wiggled with it till I found the optimal depth in this situation which was 10.
To get more insight on how the model did since Trees tend to overfit data, I then fitted a Random Tree Regressor with the depth of 10th which significantly improved my accuracy to 78.62%. Not bad right?
But then in the search of better predictions, I fitted a couple more models which I highly recommend, it's a fun process I promise.
So I fitted Gradient Boosting Regressor and tweeked its hyperparametres till it did as good as the Random Forest, at this point I knew if I was to get better accuracy, it'll be only by a fraction. 
Then I fit an XGboost Regressor to see and understand how the type of model was going to perform when trained on my data, still no success to beat the Random Forest and Gradient Boosting.
To validate all of this as I mentioned above I choose MEA as an evaluation metric and that is when things became intersting and I had the best metric through the Gradient boosting model, which I choose to implement in my app to do live predicting with an MAE of 1.32 degrees Celsius.


![Crepe](/img/winddirwatertempbars.png){: .center-block :}
Visualizing what the model is predicting before droping the target!

![Crepe](/img/blobs.png){: .center-block :}
 

### Heat maps ###

Showcasing dependencies of features with most effect on the model!

![Crepe](/img/heatmapswelldirwaves.jpg){: .center-block :}

kdeplot showing the concentration of colder waters with NW winds and strong swell more than 5 feet at 8 sec intervals.
![Crepe](/img/gplot.png){: .center-block :}
Showcasing correlation between Wind Direction & Wind Speed

![Crepe](/img/winddirwindspeed.png){: .center-block :}

PDP showcasing at what point wind direction start affecting the temperature!

![Crepe](/img/pdp.png){: .center-block :}

PDP showcasing at what point wave height start affecting the temperature!

![Crepe](/img/wavepdp.png){: .center-block :}

#### We all love trees for a reason!

![Crepe](/img/treeleft.png){: .left-block :}  ![Crepe](/img/treerught.png){: .right-block :}

#### Creating an interactive app with Dash with deployment to Heroku

To not overwhelm you, I will share steps on doing so in a seperate post since I'm focusing in Regression Modeling, 
But for now you can check the link to my app [oceanai17](http://oceanai17.herokuapp.com/predictions)



The code to make a pipeline:


```javascript
#after importing all neccesary encoders, imputers and model!

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


_(Data wrangling and feature engineering linked in my github)_
[see code version here](https://github.com/MehdiKhiatiDS/DS-Unit-1-Build/blob/master/Project_Up_Welling!.ipynb)

[_Predictive modeling Link step by step :_](https://github.com/MehdiKhiatiDS/DSAI/blob/master/ocean_AI17.ipynb.zip)
Heads up: Its a bit of a big file and you'll need to unzip it!





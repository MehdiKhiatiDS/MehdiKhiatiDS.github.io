---
layout: post
title: Machine Learning Prediciting Ocean Water Temperature!
subtitle: Fitting a  Regression model.

---
##### Chooses a target, evaluation metric, and baseline for regression:
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
![Crepe](/img/clitoris.jpg){: .center-block :}



Using facets grip from Seaborn, I plotted wind direction correlating with water temperature by month, as we see the more the winds tends to gust from the north the water gets colder which is Upwelling while the south winds generate the opposit effect known as Downwelling. 

### Isn't Water supposed to be warm in May? ###
![Crepe](/img/year1seaborn.jpg){: .center-block :}
![Crepe](/img/seaboaryear2.jpg){: .center-block :}

 

### Increase of winds from NW tends to cool the water! ###
![Crepe](/img/kdeplotseabornwindwatta.jpg){: .center-block :}
kdeplot courtesy of Seaborn

### SSW and NNW winds cause the highest water temperature variances! ###
![Crepe](/img/nnw.jpg){: .center-block :}

![Crepe](/img/ssw.jpg){: .center-block :}

### October might be the best month to visit Southern California! ### 
###### Observing Water Temperature Variance Through 2018 ####### 
![Crepe](/img/seaborn%20plot.jpg){: .center-block :}

### Wind speed from NW speeds up the cooling effect!
![Crepe](/img/southwindspee.jpg)

### While wind speed from SW speeds up the warming effect!
![Crepe](/img/north%20windspeed.jpg)

The code to the Facet Plot I used to do a monthly analysis of wind direction and water temperature:
_(rest of code step by step will be linked in my github)_
[see code version here](https://github.com/MehdiKhiatiDS/DS-Unit-1-Build/blob/master/Project_Up_Welling!.ipynb)

```javascript
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
params = {'legend.fontsize': 'x-large',
          'figure.figsize': (22, 8),
         'axes.labelsize': 'large',
         'axes.titlesize':'x-large',
         'xtick.labelsize':'x-small',
         'ytick.labelsize':'medium'}
sns.set(style="ticks")
# Pulling Upwelling dataset we created fron NOAA and UCSD databases
#df = pd.DataFrame(np.c_[upwelling['Water temperature'], upwelling['Month'], upwelling['Wind Direction coordinates']],
                  columns=["Water temperature", "Month", "Wind Direction coordinates"])
# Initialize a grid of plots with an Axes for each Month
grid = sns.FacetGrid(df, col="Month", hue="Month", palette="tab20c",
                     col_wrap=4, height=5)
# Draw a horizontal line to show the starting point
grid.map(plt.axhline, y=0, ls=":", c=".5")
# Draw a line plot to show the coordinate
grid.map(plt.plot, "Water temperature", "Wind Direction coordinates", marker="o")
# Adjust the tick positions and labels
grid.set(xticks=np.arange(0,30,2), yticks=['NE', 'NNE', 'SE', 'SSE', 'SSW', 'SW', 'NW', 'NNW'],
         xlim=(0, 30), ylim=('NE', 'SW'))
# Adjust the arrangement of the plots
grid.fig.tight_layout(w_pad=1)
```

_Sources_: [NOAA](https://www.ndbc.noaa.gov), [Ocean Motion](https://www.oceanmotion.org), [UCSD](https://ucsd.edu)

[_Link for step by step coding process on github:_](https://github.com/MehdiKhiatiDS/DS-Unit-1-Build/blob/master/Project_Up_Welling!.ipynb)






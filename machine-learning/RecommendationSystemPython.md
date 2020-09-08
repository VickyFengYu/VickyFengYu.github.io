# Recommendation System

Recommender systems can be loosely broken down into three categories: content based systems, collaborative filtering systems, and hybrid systems (which use a combination of the other two).

**Content based approach** utilizes a series of discrete characteristics of an item in order to recommend additional items with similar properties.

**Collaborative filtering approach** builds a model from a user’s past behaviors (items previously purchased or selected and/or numerical ratings given to those items) as well as similar decisions made by other users. This model is then used to predict items (or ratings for items) that the user may have an interest in.

**Hybrid approach** combines the previous two approaches. Most businesses probably use hybrid approach in their production recommender systems.


![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/machine-learning/image/recommendation-system.png?raw=true)



## Popularity-based recommenders



## Evaluating similarity based on correlation

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/recommendation%20system/evaluating%20recommendation%20systems.jpg?raw=true)


![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/recommendation%20system/evaluating%20recommendation%20systems_2.jpg?raw=true)


## Classification-based collaborative filtering
So for our example when it comes to user attribute data the dataset might define key characteristics of users that purchased or did not purchase in the past. And for purchase history these datasets describe what purchases users have made or have not made in the past. You can also think of this as a type of transaction history data. A third type of data these systems can accommodate is contextual data. By using contextual features it's possible to break recommendations into unique segments based on things like hour, season, or user browser history that is tracked through cookies.##  Private Static Field  & Get Method

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/recommendation%20system/classification-based%20collaborative%20filtering.jpg?raw=true)

```
    "import numpy as np\n",
    "import pandas as pd\n",
    "\n",
    "from pandas import Series, DataFrame\n",
    "from sklearn.linear_model import LogisticRegression"
```

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/recommendation%20system/classification-based%20collaborative%20filtering%20code.jpg?raw=true)

Based on this data you use logistic regression as a classifier to recommend whether to include him in the marketing initiative. If the model predicts that he will subscribe to a term deposit upon marketing contact then he should be included. If the model predicts that he won't subscribe then he should not be contacted with the marketing offer.



##  Model-based collaborative filtering systems

let me explain to you regular singular value decomposition or SVD. SVD is a linear algebra method that you can use to decompose a utility matrix into three compressed matrices. It's useful for building a model-based recommender because you can use these compressed matrices to make recommendations without having to refer back to the complete and entire dataset. With SVD, you uncover latent variables.These are inferred variables that are present within and affect the behavior of a dataset.Although these variables are present and influential within a dataset, they're not directly observable.




The next thing we're going to do, is we're going to take this utility matrix, and transpose it, and then we're going to use SVD to decompose it down to synthetic representations,of the user reviews.



```
   "rating_crosstab.shape"
   ```

##  Content-based recommender systems

Content-based recommenders recommend an item based on its features and how similar those are to features of other items in a dataset.

The nearest neighbor algorithm is an unsupervised classifier. It's also known as a memory-based system, because it memorizes instances and then recommends an item, or a single instance,based on how quantitatively similar it is to a new incoming instance.

```
    "import numpy as np\n",
    "import pandas as pd\n",
    "\n",
    "import sklearn\n",
    "from sklearn.neighbors import NearestNeighbors"
   ```


![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/recommendation%20system/content-based%20recommender%20systems.jpg?raw=true)


##  Evaluating recommendation systems

To ascertain how reliable our models are we need to determine the quality of the predictions that they make. To do that in Python we can use scikit-learn's metrics module. Within this module you can find all sorts of functions for scoring your models and evaluating their predictive performance.

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/recommendation%20system/precision.jpg?raw=true)

```
    "import numpy as np\n",
    "import pandas as pd\n",
    "\n",
    "from pandas import Series, DataFrame\n",
    "from sklearn.linear_model import LogisticRegression\n",
    "from sklearn.metrics import classification_report"
```

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/recommendation%20system/recall.jpg?raw=true)

So we see we have a precision of 87 here, and what that means is that of all the offers that were made, 87% of them were made to users that liked them. This metric is an indicator of how precise the predictions were. When we look over at recall we see that we get an 89. And what that is really saying is of all the products that users liked, 89% of those products were offered to them.


----------

### Footnotes

[1] 
[2]

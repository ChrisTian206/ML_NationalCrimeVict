# Classification with R: National Crime Victimization 

## Data Description
The data I am using is National Crime Victimization Survey: School Crime Supplement, 2013. This data is a survey that 
asked many students on whether they have experienced a certain type of bully along with many other questions.
Data is provided to us pre-processed and cleansed. 
There are 4947 observations and 204 attributes with the last attribute being the class attribute, o_bullied.
The goal for is project is to train multiple machine learnign models that does binary classification, that is to predict is a student is o_bullied or not.

## Pre-processing
Training a model with 4947 x 204 dataframe can be very expensive. Therefore, using pre-processing methods is neccessary. Here are the 2 pre-processing methods that I consider:

### nearZeroVariants
nearZeroVariants methods eliminates attributes that has zero or almost zero variants. Using this method, the data has 125 attributes left.
### Boruta
Boruta is a more complexed way to calculate the relavant of a attribute to the class attribute. Using this method, it returns 64 confirmed important attributes with 22 tentative attributes. In total, it suggests to use 86 attributes for model training.

#### Decision:
Considering the amount of computing power is avaialable, I decide to go with nearZeroVariants method.

## Train and Test Split 
80% training, 20% testing

## Data Imbalance
With 3817 students not bullied and 1130 students bullied, this dataset is clearly imbalanced. Feeding imbalanced train data to the model can significantly impact the accuracy, TPR, TNR, ROC of our model. To fix this issue, here are 2 ways:

### Undersampling:
While have the seed being set to 123, the training dataset has 904 Yes 3053 No. Using understampling, Yes and No class will have the same number of samples in the train dataset.

### SMOTE
SMOTE algorithm generates synthetic data points based on KNN method. While setting the k to 5, I'm able to obtain 1808 samples for both class. 

#### Decision:
I decide to use SMOTE as it provides more samples for the models to train.
Train Data: 1808 Y 1808 N
Test Data: 764 Y 226 N

## Model Training and Evaluation
In conclusion, our best model is the XGBoost model. The GBM's TPR for class 0 of this model is 0.771 and the TPR for class 1 of this model is 0.673, which meets the our expectation. The XGBoost's TPR for class 0.777 and TPR for class 1 0.66. While XGBoost delivers slightly higher TPR and weighted accuracies for class 0, it falls short of TPR for class 1.
While trying to achieve high performance by tuning parameters, it’s also necessary to remember that preprocessing the initial data and training data is also important. We initially tried to use the boruta method along with tentative attributes, 86 attributes in total, to improve efficiency. But, our TPRs were limited by a specific level. Therefore, we switched to the nearZeroVar method to preserve more attributes thus keeping more information for our models to train. Because the test dataset is heavily imbalanced with significantly more N class. We introduced slightly more Y class in our train dataset to allow our models to emphasize it more. And the result proves our thought is correct. Having more Y classes in the training dataset actually boosted TPR for class 1.
Assuming the survey data is honest and ideal, there are definitely many improving spaces. If time and resources allow, we could implement and fine tune other complex algorithms. For example, XGBoost has much more parameters than those that we tuned. But tuning all parameters on our large training dataset could take up much time and resources. For GBM and XGBoost, our best model used light to moderate complexity. The problem for future thoughts would be how to further improve TPN for both classes. We are looking forward to researching and trying more ideas and ways for improvements. 

#### Gradient Boost Machine
| | | |Prediction | 
|-|-|-|-|
| Actual Class| | N | Y |
| |N | 589 | 175 | |
|  |Y| 74 | 152 | |

| | TPR | TNR | Precision | Recall | F-measure | ROC | MCC | Kappa |
|-|-|-|-|-|-|-|-|-|
| class 0 | 0.771 | 0.327 | 0.889 | 0.771 | 0.826 | 0.721 | 0.396 | 0.383 |
| class 1 | 0.673 | 0.230 | 0.465 | 0.673 | 0.550 | | | |
| Wt.Average | 0.748 | 0.305 | 0.791 | 0.748 | 0.762 | | | |

#### XGBoost
| | | |Prediction | 
|-|-|-|-|
| Actual Class| | N | Y |
| |N | 594 | 170 | |
|  |Y| 77 | 149 | |

| | TPR | TNR | Precision | Recall | F-measure | ROC | MCC | Kappa |
|-|-|-|-|-|-|-|-|-|
| class 0 | 0.777 | 0.341 | 0.885 | 0.777 | 0.828 | 0.718 | 0.392 | 0.382 |  
| class 1 | 0.660 | 0.223 | 0.467 | 0.660 | 0.547 | --- | --- | --- |
| Wt.Average | 0.750 | 0.314 | 0.789 | 0.750 | 0.763 | --- | --- | --- |

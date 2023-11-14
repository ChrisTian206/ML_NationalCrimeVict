# Classification with R: National Crime Victimization 

## Data Description
The data I am using is National Crime Victimization Survey: School Crime Supplement, 2013. This data is a survey that 
asked many students on whether they have been bullied along with many other questions.
Data is provided to us pre-processed and cleansed. 
There are 4947 observations and 204 attributes with the last attribute being the class attribute, o_bullied.
The goal for is project is to train multiple machine learnign models that does binary classification, that is to predict is a student is bullied or not.

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


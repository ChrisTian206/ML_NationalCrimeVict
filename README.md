# ML_NationalCrimeVict

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

#### I decided to go with nearZeroVariants.

## Train and Test Split 

## Data Imbalance
With 3817 students not bullied and 1130 students bullied, this dataset is clearly imbalanced. Feeding imbalanced train data to the model can significantly impact the accuracy, TPR, TNR, ROC of our model. To fix this issue, here are 2 ways:

### Undersampling:


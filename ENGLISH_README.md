# WineQuality
Solving the Cognitivo.ai challenge

The present problem refers to the Portuguese wines "Vinho Verde" database, which have variants of white and red wine. Due to privacy issues, only physical-chemical (input) and sensory (output) variables are available. The variables present are:

> 1. Fixed acidity: amount of acids involved in wine that are fixed or non-volatile.
   
 > 2. Volatile acidity: the amount of acetic acid in wine, which at very high levels can lead to an unpleasant taste.

 > 3. Citric acid: found in small amounts, citric acid can add 'freshness' and flavor to wines
 
 > 4. Residual sugar: the amount of sugar remaining after fermentation. It is rare to find wines with less than 1 gram / liter and wines with more than 45 grams / liter are considered sweet.
  
 > 5. Chlorides: the amount of salt in the wine
 
 > 6. Free sulfur dioxide: the free form of SO2 exists in equilibrium between molecular SO2 (as a dissolved gas) and the bisulfite ion; prevents microbial growth and oxidation of wine.

> 7. Total sulfur dioxide: amount of free and bound forms of S02; at low concentrations, SO2 is mainly undetectable in wine, but at SO2 free concentrations above 50 ppm, SO2 becomes evident in the nose and flavor of the wine.

> 8. Density: the density is close to that of water, depending on the percentage of alcohol and sugar.

> 9. pH: describes how acidic or basic a wine is on a scale from 0 (very acidic) to 14 (very basic); most wines are between 3-4 on the pH scale.

> 10. Sulfates: additive for wine that can contribute to the levels of sulfur dioxide gas (S02), which acts as an antimicrobial and antioxidant.

> 11. Alcohol: the percentage of wine's alcohol content

## a. How was the definition of your modeling strategy?

The work is carried out considering 4 main steps:
1. Data cleaning;
2. Exploratory analysis;
3. Modeling;
4. Comparison.

Within these steps, some subroutines are extremely important:
1. Data cleaning:
    - Outliers identification;
    - Use of the Z-score method to remove outliers;
    - Binarization of the "type" attribute: dummy variable.
2. Exploratory analysis:
    - Creation of another column as an evaluation category: good, regular and bad;
    - Correlation analysis;
    - Pairplot analysis of the main variables;
    - Violin plot analysis of the main variables in relation to quality.
3. Modeling:
    - Separate 20% of the data to be used as validation data and 80% for training;
    - Apply StandardScaler normalizer;
    - Test regression techniques that I consider most appropriate:
      - DecisionTreeRegressor
      - KNeighborsRegressor
      - RandomForestRegressor
      - DecisionTreeRegressor
4. Comparison:
    - Comparison of test and training accuracy for each model;
    - Calculation of the 'weighted' F1-score.

## B. How was the cost function used defined?

I used the entropy cost function, commonly used in classes, since Gini should normally be used for continuous attributes. This is an important piece of information, as this option is more computationally costly (since it uses logarithmic transformation), it is common for the Gini index to be used improperly in all applications. If the classes were too unbalanced, we would have to use another methodology. More information can be found in the work of Elena Raileanu and Kilian Stoffel, * Theoretical comparison between the Gini Index and Information Gain criteria * (https://www.unine.ch/files/live/sites/imi/files/shared/documents/ papers / Gini_index_fulltext.pdf).


## C. What was the criterion used in the selection of the final model?

Unlike binary classifications, which use common error functions or simple confusion matrix, in the case of a problem of several classes, we have to use other metrics. In this case, I chose to use the accuracy in the test data and also the weighted F1-score (not to be confused with the F1-score and problems with binary target

## D. What was the criteria used to validate the model? Why did you choose to use this method?

I used two criteria: cross-validation and RMSE.

- RMSE: This is an excellent metric for regression models, as well as being very easy to interpret. The Square Root of the Mean Square Error - or simply RMSE in English - is nothing more than the difference between the value that was predicted by your model and the actual value that was observed.
- Cross validation: Cross-Validation - or Cross Validation - is a technique that aims to understand how your model generalizes, that is, how it behaves when it will predict data that you have never seen. So we create different training and test sets and we train the model and make sure it is performing well. In this case, instead of using just one test set to validate our model, we will use N others from the same data. I used the K-Fold method.

The combination of these two allows us to obtain the best validation set for a multivariate regression problem.

## E. What evidence do you have that your model is good enough?

I performed a test with a set of tests and the predicted values were identical to the target values. From the metrics presented, it is observed that in most cases, the model will cover all inputs. In some cases, you may miss the classification of 1 or 2 wines throughout the set.

It is important to note that these tests were done previously with the dirty data set, that is, with the outliers. The best result obtained in this case had been an accuracy of 60%. This highlights the importance of a correct cleaning of the data.


** ATTENTION **: In order to show how the correct choice of cost, data cleaning and scheduling functions are important, I also uploaded a file where these steps were not performed (Wine (sem wrangling - sem escalonamento) .ipynb ).


## The aim of this datathon is to predict sales of the following items on specific Ryanair flights: 
- Ham_Cheese_Panini_qt
- Chicken_seeded_Panini_qt
- Ham_Cheese_Croissant_qt
- Fresh_sandwich_qt
- Choc_Croissant_qt
- Chicken_seeded_sandwich_qt. 

## Missing data: 

Categorical missing data:  
Was filled using various API's found on the internet. This is why we need the airports.json and countries.json

Numerical missing data: 
'dep_delay' was filled by training a KNN for predicting the values. 
Missing values in the y variables (food items) were dealt with by training a RandomForest model to predict the quantities sold for each item that were missing. This enhanced our scores by a mile. 

## Incoherence in flight sequences. 

Some flight sequences did not make sense. You can see this in the 'real vs planned lofs_1_year.xlsx'. Example: The same aircraft would do PAR/MAD - BCN-VLL. 
But the aircraft should logically leave from MAD in the second flight, since that is where it landed. So we created a code capable of detecting these sequence inconsistencies. 
When training, we tried removing these inconsistent sequences vs keeping them, and found better scores when removing them. 

## Outliers

We removes outliers that were purely impossible. Like 12 hour flights because we know that Ryanair (at least for this dataset) only operates inside europe and occasionally Morocco. 
So max flight time was 6 hours. 
Since we have many outliers we decided to apply log transformations to right-skewed variables which brought down the number of outliers. 

## Models tried

We tried a bunch of classical ML approaches, as well as Deep learning models, but the two best models we found were Catboost and XGboost. 
Best scores (Catboost), averaged accross all items: 
Overall Average RMSE: 0.927
Overall Average MAE: 0.408
Overall Average MAPE: 20.812

This is for the training data that was given, in 'train_test.csv'. Our job was to then predict for 'final_predict_november.csv', for those specific flights. And Ryanair would then evaluate us. 


## Future recommendations

Use ensemble models. 
Try KNN for predicting and filling missing y values. Takes a monster time to run without GPU but could be more efficient. 







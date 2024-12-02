# Model Card

For all the models trialled, the inputs and output are the same data split into train, test and validation sets.

**Raw Data Sources**

**Input:** Weather Dataset from Kaggle - Source unknown. 45,420 rows with 33 variables across 5 locations.

**Output:** Generator Real power (kW) from the Customer Endpoint Hourly Export Dataset, produced by the National Grid. This dataset contains 52,352 rows across 10 locations.

Through the process of matching the locations and the Datetime value across two datasets reduced the combined dataset to 12330 rows. The combined dataset is then are then split into train, test and validation data sets. The training data set is size 7398.

More details on the data for these models can be found on the data card.

The Random Forest Model has the best RMSE value of all the models.

## Model 1

The first step is to use Principal Component Analysis (PCA) to reduce the number of variables as a K-Nearest Neighbour Model is vulnerable to data sets with high dimensionality.

### PCA

**Input:** 30 weather variables with standard scaling applied.

**Output:** 11 PCA variables

**Model Architecture:** A linear Kernal PCA with 11 components.

### Performance

Of the 4 KNN models tested, the Linear PCA had the lowest reconstruction error of 0.045630.

Using PCA has reduced the number of components from 30 to 11, while maintaining 95% of the data variance.

### KKN

**Input:** 11 PCA Modelled weather variables

**Output:** Generator Real power (kW)

**Model Architecture:** Using the elbow method K =15

### Performance

Across all models created in this project, the Root Mean Squared Error (RMSE) is the main performance indicator used to compare the performance of each regression model. It measures the average difference between values predicted by a model and the actual values.

The RMSE value of the KNN model is 0.409804.

Figure 1 shows the predicted values of data points on the x-axis and the error difference between the predictions and the real value on the y-axis.

![Figure 1: KNN Residual Errors](KNN_residual_errors.png)

### Limitations

The KNN model needs the use of PCA due to its sensitivity to high dimensional data, but PCA removes the ability for people to transparently interpret how the data affects the power generation of Solar Panels.

### Linear Regression

During the EDA the data sets showed a strong linear trend, so fitting a simple linear model is a good idea. This model will use less computational power than other models, so if the accuracy is comparable. Then it would be the better model to be used. This model also gives us a benchmark performance comparison value to compare with other models.

**Input:** 11 PCA Modeled weather variables

**Output:** Generator Real power (kW)

**Model Architecture:** Default value model

### Performance

The RMSE value of the Linear Regression model is 0.4233267.

Figure 2 shows the predicted values of data points on the x-axis and the error difference between the predictions and the real value on the y-axis (Residual Error).

![Figure 2: Linear Model Residual Errors](LinearMod_Residual Errors.png)

### Limitations/Trade-Offs

The linear regression model predicted negative values as shown on the x-axis of Figure 2. The Real power generation value can not be negative. This could have been solved with a rule that made any negative value predicted to be replaced by 0. But this, combined with the highest initial RMSE value out of the models fitted on the data, supported the decision not to do any further optimisation of this model.

## Model 2 - Random Forest Decision Tree Model

### Random Forest 

**Input:** 30 Weather Variables

**Output:** Generator Real power (kW)

**Model Architecture:** Random Forest Model bootstrap = 'False', Max_depth = 20, max_features = 'Sqrt' and n_estimators = 300.

### Performance

The RMSE value of the Random Forest model on the validation data is 0.352396.

The Random Forest Model has the best RMSE value of all models.

The Model Architecture was found using a grid search optimisation.

Figure 3 shows the predicted values of data points on the x-axis and the error difference between the predictions and the real value on the y-axis. When comparing Figure 3 to previous residual error plots, remeber the data for the previous models has been smcaled.

![Figure 3: Random Forest Residual Errors](RandomForest Residual error.png){alt="Figure 1: KNN Residual Errors"}

# HW3

## Q1: What causes what?

1.  Because we don't know what causes what. We cannot tell whether more police lead to lower crime or higher crime leads to more police. What we can only say is that there may exist some correlation between police and crime. If we could do an experiment with random assignment pf cops in some place and see the crime rate of that place, we would know if there exists a causation.

2.  They found a natural experiment to isolate the effect and used terrorism alert systems. When there is a high alert, more cops would be placed in the streets, which is unrelated with crime. And the researchers collected the crime data and the related alert situation. In the table, days with the higher alert have lower crimes. The coefficient is statistically significant at the 5% level. And controlling for the METRO ridership reduces the impact of police on crime.

3.  They controlled for the ridership because during the high alert day, if less people are out, there will be fewer opportunities for crime, so the crime will be lower. This effect is not caused by the police. Therefore, we need to control. After controlling, we can capture the relationship of police on crime sorting out the impact of people going out.

4.  The model uses the interaction between distractions and high alert days and estimates whether the effect of high alert day on crime was the same in different districts. The results show that the effect only exists clearly in district 1 and is statistically significant at the 1% level. In other districts, the effect is still negative but very small and statistically insignificant.

## Q2: Tree modeling: dengue cases

The model we use as following:

total_cases \~ specific_humidity + tdtr_k + precipitation_amt

First, split into training and testing data.

### CART

1.  Fit the model on the training data and get a big tree.

![image](https://user-images.githubusercontent.com/112587000/228054788-061c272e-09e2-4205-9a99-8012a5ada7e7.png)

2.  Then, based on the 1SE rule, find the best cp and prune the tree.

The best cp:

![image](https://user-images.githubusercontent.com/112587000/228054941-e2e8e5b7-2330-40fc-892a-89e829f8526f.png)

The the pruned tree:

![image](https://user-images.githubusercontent.com/112587000/228055020-2a9825ee-653a-4199-b592-27487a26a93d.png)

3.  Prediction on the test set.

4.  RMSE:
[1] 37.91261

5.  Plot the Partial Dependence Plot.

Partial dependence of total cases on specific_humidity:

![image](https://user-images.githubusercontent.com/112587000/228055304-683da0ca-f298-4933-aa39-86c440af824e.png)

Partial dependence of total cases on tdtr_k:

![image](https://user-images.githubusercontent.com/112587000/228055385-3d46d932-9be5-4dca-8dc5-e76566ffa6c0.png)

Partial dependence of total cases on precipitation_amt:

![image](https://user-images.githubusercontent.com/112587000/228055482-b6251f8b-f72c-4cff-bb14-30f82874998d.png)

### Random forests

1.  Fitting Random Forest to the train data set

Shows out-of-bag MSE as a function of the number of trees used:

![image](https://user-images.githubusercontent.com/112587000/228055821-af8a13d8-79d5-453d-a1ad-3f3aac6bac61.png)

2.  Prediction

3.  RMSE on the test set:
[1] 25.42312

4.  Plot the Partial Dependence Plot.

Partial dependence of total cases on specific_humidity:

![image](https://user-images.githubusercontent.com/112587000/228056035-d2435176-c345-47e1-b138-be8ef648b26a.png)

Partial dependence of total cases on tdtr_k:

![image](https://user-images.githubusercontent.com/112587000/228056093-5c85f959-c52c-4a39-a430-54b1aa4f5ffd.png)

Partial dependence of total cases on precipitation_amt:

![image](https://user-images.githubusercontent.com/112587000/228056201-1ea3dda7-2bd7-491d-9102-0a3ccf1af06f.png)

### Gradient-boosted trees

1.  Fit the gbm model

![image](https://user-images.githubusercontent.com/112587000/228056439-fe9b5422-f1f8-4901-b40d-6fd625151ba3.png)

2.  Find the best ntree and prune.

ntree:

![image](https://user-images.githubusercontent.com/112587000/228056526-f749d434-628e-413d-8ae9-c58341fb7e78.png)

number of tree
[1] 131

Then use the best ntree.

3.  Prediction

Predict on testing data.

4.  RMSE:
[1] 36.62508

5.  Plot the Partial Dependence Plot

Partial dependence of total cases on specific_humidity:

![image](https://user-images.githubusercontent.com/112587000/228056830-e18334d5-c9c6-4794-b8eb-7004ae532fc2.png)

Partial dependence of total cases on tdtr_k:

![image](https://user-images.githubusercontent.com/112587000/228056893-6a50f2eb-7cfa-45f4-bbcc-f02b10e0ebe0.png)

Partial dependence of total cases on precipitation_amt:

![image](https://user-images.githubusercontent.com/112587000/228056942-b645aa85-c104-4712-b09c-a522f82e52c1.png)

### Compare RMSE on the test set:
[1] 37.91261

[1] 25.42312

[1] 36.62508

Comparing the RMSE, the random forest performs best on the test set with the lowest RMSE.

## Q3: Predictive model building: green certification

### Introduction:

To build the best predictive model possible for revenue per square foot per calendar year, and to use this model to quantify the average change in rental income per square foot associated with green certification, I used variable selection, tree, random forest to find the best model.

### Data:

First, I set revenue = Rent*leasing_rate(%) to show the revenue per square foot per year. And green certified was shown as green_rating.
For these variables, I dropped CS_PropertyID, Rent, leasing_rate, LEED, Energystar, cluster, net, cd_total_07, hd_total07. Because some of them doesn't relate to revenue, and some of them relate to other variables, if we add them in the model, it will be overlapped.

### Method:

I separately test five models: tree, random forest, linear model, liner model with two-way interactions, gbm. 

1.tree

![image](https://user-images.githubusercontent.com/112587000/228060145-847eeea2-c58b-4b9a-8a8c-6481d88602f8.png)

2.random forest

![image](https://user-images.githubusercontent.com/112587000/228060188-bf3f5ae5-d451-4921-b674-fa57069464bf.png)

![image](https://user-images.githubusercontent.com/112587000/228060231-37d68556-905a-4528-8478-4c060424b876.png)

![image](https://user-images.githubusercontent.com/112587000/228060256-d7347b95-63d0-4975-a9ce-b27c8ac9d0d8.png)

![image](https://user-images.githubusercontent.com/112587000/228060298-f1cafa51-2ca6-4e2c-ab47-feadf46c0f52.png)


3.liner model

![image](https://user-images.githubusercontent.com/112587000/228060682-71a97de6-2c67-4acf-a9a9-0a8c17487f65.png)

4.liner model with two_way interactions

The model is:

lm(formula = revenue ~ size + empl_gr + stories + age + class_a + 
    class_b + green_rating + amenities + total_dd_07 + Precipitation + 
    Gas_Costs + Electricity_Costs + City_Market_Rent + size:City_Market_Rent + 
    empl_gr:Electricity_Costs + stories:class_a + green_rating:amenities + 
    total_dd_07:City_Market_Rent + size:Precipitation + size:amenities + 
    age:green_rating + size:age + empl_gr:Precipitation + amenities:Electricity_Costs + 
    stories:Gas_Costs + amenities:Gas_Costs + amenities:Precipitation + 
    age:total_dd_07 + age:City_Market_Rent + empl_gr:Gas_Costs + 
    total_dd_07:Precipitation + age:Precipitation + class_a:Gas_Costs + 
    class_a:Electricity_Costs + class_a:total_dd_07, data = green_train)

5.gbm

![image](https://user-images.githubusercontent.com/112587000/228060395-67de9b7f-e30d-4c5b-b8e5-3bae7f85462e.png)

Then I test RMSE for these models, the result shows that random forest has the min RMSE = 6.72, so we choose random forest as our model.
For random forest model, I take variable importance measures to show that how much does mean-squared error increase when we ignore a variable, and calculate the average change in rental income per square foot associated with green certification with partial dependence plot.

### Result:

RMSE

> modelr::rmse(green.tree, green_test)

[1] 8.735821

> modelr::rmse(green.forest, green_test)

[1] 6.716499

> modelr::rmse(lm_medium, green_test)

[1] 10.37368

> modelr::rmse(lm_step, green_test)

[1] 9.745055

> modelr::rmse(green_gb, green_test)

[1] 7.740721

I choose random forest as my model, and green certification have positive effect on the average change in rental income per square foot.


## Q4

First, we split the sample into training and testing. We start with the linear regression that we're most familiar with. We get our model1: linear model. After linear model, it comes to the CART model, and we plot its cross-validated error plot. 

![image](https://user-images.githubusercontent.com/112587000/228065599-a0e13494-4fda-4434-98f5-2bb6b8067d7c.png)

Then here a convenient function to pick the smallest tree whose CV error is within 1 standard error of the smallest value. And using this function we prune our tree at the 1se complexity level. Next we use the random forests. We also plot the out-of-bag MSE as a function of the trees #.

![image](https://user-images.githubusercontent.com/112587000/228065669-c0642b43-d3a0-46de-b838-61ef198bcf29.png)

Last we use the gradient-boosted trees. 

![image](https://user-images.githubusercontent.com/112587000/228065757-e48a1b0d-cb70-435b-8e58-e60b0086a694.png)

After finishing all these models, we calculate their RMSE to represent an estimate for the overall out-of-sample accuracy of your proposed models and summarize them into a chart. 

![image](https://user-images.githubusercontent.com/112587000/228068774-9cda548d-986b-4772-977f-d3b9b43383c9.png)

After comparison, we find that Gradient Boosting trees has the smallest RMSE. So we choose Gradient Boosting trees to be our best predictive model.

a plot of the original data, using a color scale to show medianHouseValue (or log medianHouseValue) versus longitude (x) and latitude (y).

![image](https://user-images.githubusercontent.com/112587000/228069143-219b568e-3d8a-4d58-ba26-73f155909a8a.png)

a plot of your model's predictions of medianHouseValue (or log medianHouseValue) versus longitude (x) and latitude (y).

![image](https://user-images.githubusercontent.com/112587000/228069217-54d9e605-f8d4-47ec-9cde-5f1f3770bde6.png)

a plot of your model's errors/residuals (or log residuals) versus longitude (x) and latitude (y).

![image](https://user-images.githubusercontent.com/112587000/228069312-30b49617-0478-4cdd-90e9-3cd55fca397a.png)


# An exploration of the Iris dataset using two algorithms.

### Introduction
Using the Iris dataset and two algorithms, k-means clustering and logistic regression 
this project sets out to use the algorithms to classify the three species of iris contained 
within the dataset. The project builds a k-means cluster classifier, finding that k=3 is the 
optimal value for k, and a logistic regression model that provides 98% accuracy. The 
project also reports on the use of Lime to explain how the regression model made the 
classification decision.

### IMPLEMENTATION OF K-MEANS CLUSTERING
The first task to complete when implementing a clustering algorithm is to determine the 
number of clusters that is optimal for the dataset/problem at hand. Here it may seem 
intuitive that 3 clusters will be the correct number of clusters, as there are 3 species that we 
are trying to classify, however this apparent rule of thumb would not always hold, especially 
if/when the data is less segregated than this dataset it.

The number of clusters is a significant value that needs to be carefully selected. It is possible 
to select this value using several methods, a popular method is known as the elbow method, 
whereby a range of possible values are plotted for k against the WCSS and where the lowest 
value of WCSS is found, when considered against the number of clusters, whereby keeping 
the k small is preferable a value is found. The preferred measure of K-means accuracy is WCSS, 
the within cluster sum of squares. Once the value for k has been chosen the model can be built (again) and visualized by 
plotting the clusters and the computed centroids.

![image](https://github.com/tj2904/iris-kmeans-logistic/assets/3164936/e0f2bfb1-ad6f-4625-aa76-4b9c6f19643f)

While k-mean clustering isn’t a true classification algorithm, it can be used as one with 
supervised learning, as we have been doing. Therefore, we can present a confusion matrix
and a classification report.
```
               precision    recall  f1-score   support

           0       1.00      1.00      1.00        19
           1       0.78      0.93      0.85        15
           2       0.92      0.75      0.83        16

    accuracy                           0.90        50
   macro avg       0.90      0.89      0.89        50
weighted avg       0.91      0.90      0.90        50
```
![image](https://github.com/tj2904/iris-kmeans-logistic/assets/3164936/47ec84b3-0bc3-4fb5-b069-c85404dafd7d)

These both demonstrate that the algorithm does a good job of classifying, overall 
achieving 90% accuracy and performing worst for the class 2 species, where the data is 
more overlapping.

### IMPLEMENTATION OF LOGISTIC REGRESSION
For regression the labels were numerically encoded, so that 0 = setosa, 1 = versicolor and 2 
= virginica.
Following the encoding, the data was split into train and test sets. This was done with a 
value of 0.33 so that two thirds of the data was used for training and one third was held 
back for testing, this is done using random sampling so that the sets are not composed of, 
for example the first 1/3 of observations. This is particularly important in this 
dataset as the data was grouped by species. The class labels were also split out into train 
and test sets, as these will form the target for the model.

The model is then fitted to data before the resulting model is used to make predictions 
about the test stets classification. From the test set we can calculate some performance 
metrics, first the accuracy score, expressed as a percentage. We can see that this 
model performed with 98% accuracy.

```
              precision    recall  f1-score   support

           0       1.00      1.00      1.00        19
           1       0.94      1.00      0.97        15
           2       1.00      0.94      0.97        16

    accuracy                           0.98        50
   macro avg       0.98      0.98      0.98        50
weighted avg       0.98      0.98      0.98        50
```
![Untitled](https://github.com/tj2904/iris-kmeans-logistic/assets/3164936/fb28fe38-904b-429f-932d-b7607c06ec10)

### EXPLAINABILITY
By passing the data and the model into the Lime explainer we are presented with 
values that indicate which of the possible factors (in this small dataset that is all of the 
features) have an impact on the classification, and in which regard they influence that 
classification, and in which direction.
![image](https://github.com/tj2904/iris-kmeans-logistic/assets/3164936/05fda213-0cf3-43c0-a809-05f556d6b533)

### DISCUSSION OF THE RESULTS
The above implementations both demonstrate that it is possible, with a good degree of 
accuracy to identify an iris from petal and sepal width and length. While not attaining 100% 
accuracy for all three species, logistic regression provided an average, or overall accuracy of 
98% which compares favourably with the 90% accuracy attained by the k-means algorithm. 
Both LG and K-means clustering we able to correctly identify all of the versicolor species as 
it was demonstrated that this species was linearly separable from the other two. There is a 
chance, however, especially with a small dataset such as this one that the models suffer from 
overfitting. 
Overall, the logistic regression model has the better performance characteristics of the two.

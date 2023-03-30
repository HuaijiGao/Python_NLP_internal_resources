# Text Classification Task II

## Cross validation

### Development Test Sets ("Devsets") and Cross-validation

- When building a machine learning model, we want to evaluate its performance on a test set that is completely separate from the data used to train the model. 
- However, in order to tune the model's hyperparameters and make other decisions during the development process, we need another dataset to experiment on. 
- This is where the development test set, or "devset," comes in.

- The general rule is to train on the training set, tune on the devset, and report the final performance on the test set. This helps to avoid overfitting the model to the test set and gives a more conservative estimate of its performance. However, there is a paradox here: we want to use as much data as possible for training, but we also need a sizable devset to accurately evaluate the model's performance.

This is where cross-validation comes in. With cross-validation, we perform multiple splits of the data into training and dev sets, train the model on each split, and evaluate its performance on the corresponding devset. We then pool the results over the splits to compute a final dev performance metric. This helps to address the issue of having limited data for training and dev, and gives a more robust estimate of the model's performance.

To perform cross-validation, we typically split the data into k folds, with k typically ranging from 5 to 10. We then iterate through each fold, using it as the devset and the remaining k-1 folds as the training set. We train the model on the training set, evaluate its performance on the devset, and record the performance metric. We repeat this process for each fold, and then compute the average performance metric across all the folds.

|![image](https://user-images.githubusercontent.com/19381768/228710210-cee07175-f06f-4ccf-a6d9-7b7a8a69652a.png)|
|:--:|
|k-fold cross validation|


In summary, using a devset and cross-validation are important steps in the development process of a machine learning model. They help to avoid overfitting and give a more accurate estimate of the model's performance. Cross-validation in particular allows us to make the most of limited data by performing multiple splits and pooling the results.

## Evaluation with more than two classes
## Generative and discriminative Classifiers
## Logistic regression
## Cross entropy loss
## Stochastic gradient descent
## Regularization
## Multinomial logistic regression
## Avoiding harms in classification

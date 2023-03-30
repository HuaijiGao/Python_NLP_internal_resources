# Text Classification Task II

## Cross validation

### Development Test Sets ("Devsets")

- When building a machine learning model, we want to evaluate its performance on a test set that is completely separate from the data used to train the model. 
- However, in order to tune the model's hyperparameters and make other decisions during the development process, we need another dataset to experiment on. 
- This is where the development test set, or "devset," comes in.

|![image](https://user-images.githubusercontent.com/19381768/228711049-bb6ac36a-170d-4205-80f0-478e35b79dd1.png)|
|:--:|
|Small dataset (top) and Big dataset (bottom)|

### Cross-validation
The general rule is to train on the training set, tune on the devset, and report the final performance on the test set. 
- This helps to avoid overfitting the model to the test set and gives a more conservative estimate of its performance. 
- However, there is a paradox here: we want to use as much data as possible for training, but we also need a sizable devset to accurately evaluate the model's performance.

This is where cross-validation comes in. 
- With cross-validation, we perform multiple splits of the data into training and dev sets.
- Train the model on each split, and evaluate its performance on the corresponding devset. 
- We then pool the results over the splits to compute a final dev performance metric. 
- This helps to address the issue of having limited data for training and dev, and gives a more robust estimate of the model's performance.

### The k-fold cross-validation
- To perform cross-validation, we typically split the data into k folds, with k typically ranging from 5 to 10. 
- We then iterate through each fold, using it as the devset and the remaining k-1 folds as the training set. 
- We train the model on the training set, evaluate its performance on the devset, and record the performance metric. 
- We repeat this process for each fold, and then compute the average performance metric across all the folds.

|![image](https://user-images.githubusercontent.com/19381768/228710404-c93b39c9-68ad-4223-a12d-3a5cebbad23e.png)|
|:--:|
|The k-fold cross validation|

## Evaluation with more than two classes

### Confusion Matrix for 3-class Classification
In machine learning, a confusion matrix is a table that is used to evaluate the performance of a classification model. It is especially useful when dealing with multi-class classification problems, such as when we have three classes. In this case, the confusion matrix will be a 3x3 table, with rows and columns corresponding to the three classes.

- The confusion matrix is constructed by comparing the predicted labels of the model with the actual labels.
- The cells of the table represent the number of instances that were classified correctly or incorrectly.
- Specifically, the diagonal cells correspond to instances that were classified correctly, while the off-diagonal cells correspond to instances that were misclassified.

Once we have the confusion matrix, we can compute various performance metrics, such as precision and recall, for each of the three classes. However, in order to get an overall performance metric for the model, we need to combine these metrics into a single number.

There are two common ways to do this: macroaveraging and microaveraging. With macroaveraging, we compute the performance metric for each class separately, and then average over the classes. For example, we would compute the precision and recall for each of the three classes, and then take the average of these six numbers.

With microaveraging, we collect the decisions for all classes into one confusion matrix, and then compute the precision and recall from that table. This means that we combine all the true positives, false positives, and false negatives across the three classes. We then compute the precision and recall based on these combined numbers.

Let's look at some examples to see how this works. Suppose we have a 3-class classification problem, with classes A, B, and C. We train a model and evaluate its performance on a test set, and obtain the following confusion matrix:

|        | A      | B      | C      |
|--------|--------|--------|--------|
| A      | 10     | 2      | 3      |
| B      | 1      | 8      | 0      |
| C      | 0      | 1      | 9      |

To compute the precision and recall for each class, we look at the rows and columns of the confusion matrix. For example, the precision of class A is computed as TP_A / (TP_A + FP_A), where TP_A is the number of true positives for class A, and FP_A is the number of false positives for class A. Similarly, the recall of class A is computed as TP_A / (TP_A + FN_A), where FN_A is the number of false negatives for class A.

Using these formulas, we can compute the precision and recall for each of the three classes. For example, the precision and recall for class A are:

Precision_A = 10 / (10 + 2 + 3) = 0.625
Recall_A = 10 / (10 + 1 + 0) = 0.909

We can then compute the precision and recall for classes B and C in the same way. Once we have these six numbers, we can compute the macro-averaged precision and recall by taking their average, or the micro-averaged precision and recall by combining the true positives, false positives, and false negatives across all classes and computing the corresponding metrics.

In summary, the confusion matrix is a useful tool for evaluating the performance of a classification model, especially when dealing with multi-class problems. To combine the precision and recall for multiple classes into a single metric, we can use macroaveraging or microaveraging, depending on our needs.

## Generative and discriminative Classifiers
## Logistic regression
## Cross entropy loss
## Stochastic gradient descent
## Regularization
## Multinomial logistic regression
## Avoiding harms in classification

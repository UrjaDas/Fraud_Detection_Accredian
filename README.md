                                         ## Fraud Detection ##


                                          
## Description: ##
The goal of this project is to identify fraudulent behavior. It is a supervised binary classification problem. The Dataset consists of ten independent features and one 
dependent feature 'isFraud'. Data Cleaning, i.e., missing values, the transformation of the dataset, and dealing with the issues of outliers and multicollinearity has been 
done. The cleaning process is described after each significant step in the notebook. After doing some exploratory data analysis and data visualization, supervised machine 
learning models like Logistic Regression, Decision Tree, Random Forest, K-Nearest Neighbors, Support Vector Machines, and Deep Learning models like Artificial Neural 
The network has been implemented by making use of TensorFlow with functional Keras API. After model implementation, the performance of each model was evaluated using 
different metrics. Artificial Neural Networks gave good results on both the training and test datasets.


## Data Preprocessing:  ##
* This is a large dataset consisting of 63,62,620 entries and there are 10 independent features and one dependent feature namely 'isFraud.
* There are no null values present along any of the features and hence does not need any preprocessing along that line.
* The feature 'step' just contains maps of a unit of time in the real world and thus is not indicative of any pattern in the data.
* Transform the Dataset: From the analysis, we could observe that the dataset is highly imbalanced and hence needs to be preprocessed.
* The entry corresponds to be of fraudulent type only when the type is either CASH_OUT or TRANSFER, hence we transform the dataset such that it contains only
  those entries which have either of the two types mentioned.
* The new dataset consists of 27,70,409 entries and 9 independent features.
* There is an almost equal number of Fraudulent cases in both the types: TRANSFER and CASH_OUT. However, the total number of Non-Fraudalent cases is much more
   in the CASH_OUT type transaction in comparison to the TRANSFER type.
* On exploring the feature 'nameOrig' which represents the name of the customer who started the transaction, it was realized that only in a few cases the transaction
  was started by the same customer. Also, I checked the number of times the transaction was started more than once by the same customer in the case of fraudulent cases
  and realized that no two cases that were fraudulent were repeated by the same person. It therefore is not indicative of any pattern that could be helpful in prediction.
  The feature was therefore dropped.
* The feature 'isFlaggedFraud' consists of only 16 entries corresponding to category 1 and the rest all are 0. On further analysis, it is seen that all these 16 entries
  also correspond to category 1 in the 'isFraud' feature. Hence we can deduce that if there is a 1 in the isFlaggedFraud category then it guarantees the case of Fraud
  (completely correlated) and hence can be useful while making predictions. So this column is not dropped and left as it is.
* On analyzing the feature 'nameDest' which stores information regarding the customer who is the recipient of the transaction, it was realized that there were around 5
  lakh unique recipient IDs amongst a total of around 27.5 lakh transactions. This implies that the recipient account is repeated in certain transactions. This can be
  important in deriving insights about the patterns since it is very likely for the scammers to repeat the process with different customers and hence the destination
  account could be the same in many cases.
* It would therefore not be wise to drop this column altogether like we did for the 'nameOrig' feature. Hence to capture the information, a new column called count_dest
  has been created which stores the number of times a particular destination account has been encountered during different transactions. After creating this column, the
  original column 'nameDest' has been dropped.
* There are also cases where the destination account happens to be the same in different transactions where some transactions have been classified into fraud and some
* into non-fraud. Hence 'count_dest' might not be the best to understand and therefore it was dropped later.
* After analyzing the feature 'newbalanceOrig', we can see that in most of the fraudulent cases, the new balance of the customer is 0 as expected.
* However there are instances where the amount left in the customer's account lies far away from 3 standard deviations (outliers), but since the dataset is highly
  imbalanced dropping these outliers could significantly impact the model's prediction abilities and accuracy. Therefore it would be wise to not make changes or drop
  rows for now.
* There are entries where the original balance is 0 but there is some amount transaction that is shown along the 'amount' column which does not seem right to me. So I
  have removed such rows from the dataset as it could create some discrepancies.
* Since a lot of fraud category data points lie as outliers for the feature 'oldbalanceOrg' it would be difficult to remove the outliers as it could impact the accuracy.
* Another insight is that the transactions done through the 'TRANSFER' method are on accounts with high old balance amounts while the CASH_OUT type transaction is done
  on accounts with lower original balance.
* There are two kinds of cases, one where the final balance in the destination account is 0 and one where it is not 0.
* The cases where the destination account has 0 amount are mostly where the transactions are done through the 'TRANSFER' method and in the situation where there is some
  amount in the destination account, the transactions have been done through the 'CASH_OUT' method.
* Most of the outliers pertaining to the feature 'newbalanceDest' are associated with non-fraudulent cases which shows that in most of the fraudulent cases the new
  balance of the destination account is kept low.
* Through the correlation heatmap we could see that the two features, namely 'oldbalanceDest' and 'newbalanceDest' are highly correlated so it can be a good idea to
  drop one of the two features, since it can lead to the problem of multicollinearity and create biases in prediction.
* On analyzing the feature 'amount' we understood that most of the outliers belonged to the non-fraudulent category . Further analysis showed that those outliers lie
  many standard deviations away. So I decided to remove the outlier which was further than the maximum amount value categorized as the fraudulent class (2443 rows)
  since it can still keep intact the information necessary for prediction.


## Metric For Evaluation ##
  * Since it's a classification problem, various metrics like accuracy score, recall score, precision score, f1 score, classification report, and confusion matrix were
    determined to evaluate the performance of different models. However, this is a case where the dataset is highly imbalanced hence metrics like accuracy score and
    precision score could not give a good idea about how well the model is performing. Recall score gives a better idea regarding the model's performance.


## Best Performing Model ##
* All the supervised machine learning models gave good accuracy and precision scores but only the decision tree could give a decent recall score (indicative that other
  models were not able to classify the fraudulent class properly).
* Artificial Neural Networks gave good results on both the training and test datasets. This might be because neural networks especially deep neural networks are highly
  capable of capturing complex patterns in the data since they can automatically learn a hierarchal representation of features which can be important when dealing with
  non-linear relationships in the data.
* It gave a high recall score(0.997) along with the other metrics which shows that it could correctly identify most of the Fraud cases.


  

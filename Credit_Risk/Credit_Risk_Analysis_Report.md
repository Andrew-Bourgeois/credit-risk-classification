# **Module 20 - credit_risk_classification - Report**

## **Overview of the Analysis**

In this section, describe the analysis you completed for the machine learning models used in this Challenge. This might include:

* **Explain the purpose of the analysis.**
* **Explain what financial information the data was on, and what you needed to predict.**
* **Provide basic information about the variables you were trying to predict (e.g., `value_counts`).**
* **Describe the stages of the machine learning process you went through as part of this analysis.**
* **Briefly touch on any methods you used (e.g., `LogisticRegression`, or any resampling method).**

The purpose of this analaysis was to build a model which can be used by a lender to predict the creditworthiness of a new borrower based on certain borrower features.

In order to teach, and subsequently test, our data model we used a preiously aggregated dataset from a peer-to-peer lending services company. The dataset encompassed the following features and outcome for each record: 'loan_size', 'interset_rate', 'borrower_income', 'debt_income', 'num_of_accounts', 'derogartory_marks', 'total_debt', and 'loan_status'. Using the sample dataset features we need to create a model which can consistently predict the same outcome as the data in the 'loan_status' column, given the same corresponding features data.

To test our model's accuracy and precision we used the provided outcomes in the 'loan_status' associated with each record. After separating the outcomes data into a new Series and using the 'value_counts' method, we were able to determine the volume of loans which were 'Healthy (0)' and 'High-risk (1)' in the dataset. We were then able to use this known outcome data to later compare our model results to for determining accuracy and precision.

To create the machine learning model the first step was to import the cleaned, previously aggregated data with known outcomes into (in our case) a Pandas DataFrame. Next we needed to separate the known outcomes (y) from their correlating features (X), by copying the 'loan_status' data to a new Series and then drop them from the original dataaset. We then further divided each into an X/y Training and X/y Test set. Using the Training and test X datasets we could normailize the data as needed, trained the model using the the X/y Training datasets, and subsequently tested and verified it using the test datasets. As a last step we used a 'balanced accuracy score', 'confusion matrix', and 'classification report' to deteremine the accuracy/precision of each model and compared them.

We used various algorithms and methods to train our datamodel. The first was the `LogisticRegression` model, using the `lbfgs` algorithm and setting the maximum allowable iterations to 200. We then used the resulting trained classifier to predict the results for the X_test sample, and compared the model test results with the known test results.

Additionally, we resampled the data using `RandomOverSampler`, in order to "rebalance" the class distribution of the minority classes. We reran the modeling using LogisticRegression to compare the results between the two models to see if the random oversampled model did a better job at predicting the outcomes.

## **Results**

* **Machine Learning Model 1:**
  Description of Model 1 Accuracy, Precision, and Recall scores.
  * Accuracy: with a balanced accuracy score of 0.952 the model performed wll overall at predicting whether a loan was likely to default or not.
  * Precision: 
    * Healthy Loan (0): 1.00 or 100%; model is able to predict a healthy loan 100% of the time.
    * High-risk Loan (1): 0.85 0r 85%; model is able to predict a possible default loan 85% of the time. Another way to state is it failed to predict a known high-risk loan, but did not necessarily predict it as a healthy loan.
  * Recall: 
    * Healthy: with a recall of 0.99 the model correctly "identified" almost all of the known healthy loans from the data set.
    * High-risk: with a recall of 0.91, the model struggled a little more with "finding" the known high-risk loans, but in general did well.


* **Machine Learning Model 2:**
  Description of Model 2 Accuracy, Precision, and Recall scores.
  * Accuracy: The resampled dataset showed an imporvement to the balanced accuracy score, with a 0.995.
  * Precision:
    * Healthy (0): with a score of 0.99, there is not a true statisticla difference in predicting a healthy loan.
    * High-Risk (1): but, with a new score of 0.99, the resampled data model is much better at accurately predicting the high-risk loans.
  * Recall: 
    * Healthy (0): at 0.99, there was no change ot the recall score with the resampled data.
    * High-Risk (1): at 0.99, the resampled data model was much better at "finding" the known high-risk loans in the test dataset.

## **Summary**

* **Which one seems to perform best? How do you know it performs best?**
* **Does performance depend on the problem we are trying to solve?** (For example, is it more important to predict the `1`'s, or predict the `0`'s? )

Both models did very well at prediciting a loan which would be "Healthy (0)" as much as 100% of the time. Therefore, if a lender is going to determine their lending policy based solely on whether a loan is likely to be 'healthy' then either model is more than adequate.

If a lender's goal is to modify their lending options to a consumer based on a set of features predicting a "high-risk" loan, then the resampled data model is a much surer predictor of a 'healthy' or a 'high-risk' loan. Although, depending on the lender's risk aversion, an ~85% prediction accuracy for a high-risk loan is not unreasonable, and may offer an opportunity for the lender to require more additional info or collateral to make the outcome of the loan more "securable".

Bottom line is both models will work well depending on the risk-aversion and lending requirement criteria of the lender.
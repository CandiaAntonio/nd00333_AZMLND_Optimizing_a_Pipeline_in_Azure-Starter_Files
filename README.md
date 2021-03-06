# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Summary
The data was obtain from a direct marketing campaigns (phone calls) of a banking institution. The classification objective is to predict whether the client will open a bank term deposit (column y) using demographics as inputs.

The best performing model was the HyperDrive model with HD_127140f8-6f8f-4917-8cd5-ebdd3e3c465e_0. It derived from a Scikit-learn pipeline and had an accuracy of 0.91760. The VotingEnsemble AutoML model with ID AutoML_76196bf5-5796-412f-b294-f0e4275a60ff reach an accuracy of 0.91675

## Scikit-learn Pipeline
The steps carried out to create the Scikit-learn Pipeline:
  Creation of TabularDataset using TabularDatasetFactory
  The raw data was wrangled
  Clean data is split into train and test sets.
  From the HyperDrive runs, training the logistic regression model using arguments .
  Calculating the accuracy score.
**What are the benefits of the parameter sampler you chose?**
RandomParameterSampling was selected because it is the faster and supports early termination of low-performance runs.
**What are the benefits of the early stopping policy you chose?**
BanditPolicy stopping policy was selected because it terminates runs where the primary metric is not within the slack factor compared to the best run.
## AutoML
**In 1-2 sentences, describe the model and hyperparameters generated by AutoML.**
It was a classification task, so the primary metric that was to be maximized was set to 'accuracy'. We provided the cleaned version of the data, and number of iterations was set to a small value
## Pipeline comparison
**Compare the two models and their performance. What are the differences in accuracy? In architecture? If there was a difference, why do you think there was one?**
The two models performed very similarly in terms of accuracy. The difference could be attributed to time restriction on autoML.
The pipelines use the same data wrangling process, however autoML tests a number of scalers in combination with models, adding a preprocessing step prior to model training.

Architecturally, the models are quite different. Logistic regression (91.7% accurate; tuned with hyperdrive) effectively makes use of a fitted logistic function to carry out binary classification. The voting ensemble classifier (91.6% accurate; selected via autoML) makes use of a number of classifiers and, in this case, averages the class probabilities of each classifier to make a prediction.
## Future work
**What are some areas of improvement for future experiments? Why might these improvements help the model?**
Data is highly imbalanced
Allowing autoML running for longer time could lead to better results than Scikit learn.

## Proof of cluster clean up
**If you did not delete your compute cluster in the code, please complete this section. Otherwise, delete this section.**
compute_target.delete()

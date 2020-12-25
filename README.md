# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Summary
**In 1-2 sentences, explain the problem statement: e.g "This dataset contains data about... we seek to predict..."**

This dataset contains data about bank marketing target customer characteristics. 
We seek to predict if a custermer is willing to subscribe to a term deposit with the bank.  

**In 1-2 sentences, explain the solution: e.g. "The best performing model was a ..."**

The best performing logistic regression model was using C=0.962 as the regularization strength determining parameter and with 150 max iterations, which gave a prediction accuracy of 0.914.

## Scikit-learn Pipeline
**Explain the pipeline architecture, including data, hyperparameter tuning, and classification algorithm.**

In the pipeline, the data was ingested, cleaned and then fed into a logistic regression model for training.
Data was first ingested from an online csv file and then cleaned by one hot encoding of categorical variables.
Then logistic regression models were trained using the cleaned data and optimized by tuning parameter C and max_iter.
Parameter C was uniformly sampled in the space of 0.5-1.5
Max_iter was sampled from a integer list [50, 100, 150, 200]
The best model was then selected based on accuracy as the primary metric.

**What are the benefits of the parameter sampler you chose?**

I chose random parameter sampling strategy for C and max_iter.
C used uniform sampling because C is a continuous parameter.
Max_iter used choice because max iteration is a discrete parameter.

**What are the benefits of the early stopping policy you chose?**

I chose the early stopping policy with an evaluation interval of 1. If there is a bug in the script, this helps with terminating the run and saving time. 

## AutoML
**In 1-2 sentences, describe the model and hyperparameters generated by AutoML.**

Voting Ensemble was chosen as the best model by AutoML, with a prediction accuracy of 0.917. 

## Pipeline comparison
**Compare the two models and their performance. What are the differences in accuracy? In architecture? If there was a difference, why do you think there was one?**

The models generated by Hyperdrive and AutoML show comparable accuracy. 
In achitecture, hyperdrive used only one model, logistic regression, and optimized the model by tunning hyperparameters. While AutoML trained more than 10 models and selected the best from them. AutoML takes longer to train in this case

## Future work
**What are some areas of improvement for future experiments? Why might these improvements help the model?**

One possible improvement is to run AutoML first to narrow down the options of ML algorithms. Then use hyperdrive to fine tune the hyperparameters of one or two models selected by AutoML. This improvement may further boost the accuracy and cover a variety of ML algorithms without spending too much time on fine-tuning models that are not suitable for the dataset. 

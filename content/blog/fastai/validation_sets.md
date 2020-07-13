---
title: "Validation_sets"
date: 2020-07-10T14:30:26+08:00
slug: ""
description: ""
keywords: []
draft: false
tags: []
math: false
toc: false
---

The Validation DataSet should be carefully split based on the task at hand.

Splitting the training, validation, and test datasets at random is not always a good bet.

Before we get ahead of ourselves, let us properly define what training, validation, and test set mean.

## Definition of Datasets

All the definition of sets refers to the data at hand.

| Type of dataset | Purpose                                                                                                                                      | Remarks                                                                                                                                                                                                                |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Training Set    | <ul><li>Used to tune the model. </li> </ul>                                                                                                  | <ul> <li>For supervised machine learning tasks, this consist of the input and the output.</li> <li> For unsupervised only the input is provided.   </li> </ul>                                                         |
| Validation Set  | <ul><li>Used to check the fit of our model as it is being tuned.</li><li> Provides an indication of how well our model will generalize </li> | <ul><li> For both supervised and unsupervised tasks, only inputs are provided. </li> <li> Predictions are generated and compared with actual output or category. A score is then calculated based on the grouping</li> |
| Test Set        | <ul><li>Used to score a model in a competition or provide the final indication of model generalizability</li></ul>                           | <ul><li>Same as validation set, but only done once after tuning is done or at the end of the competition. (small subset of test is shown in competition to provide rough indication of standing)</li></ul>             |

With definitions in place, the most important thing about the validation and test dataset is that it **should be representative of the data we will see in the future**.

## Examples of how to split datasets

### Time series

For time series data, older, continuous, time series should be used to train the model.

The newer continuous dataset should be used for validation, with the newest continuous dataset reserved for testing.

### Videos and photos

Frames that are similar to each other (2 adjacent frames in a video) could be placed in the training and validation set. The result is great scores, but bad generalizability.

Why?

Because our algorithm starts to pick up on the features of the objects in the photo rather than for features that correspond to the task at hand.

## Conclusion

At the end of the day, having a good validation set will allow you to iterate quicker, and know with greater confidence, the progress that you are making.

Do not skimp on making a validation set!

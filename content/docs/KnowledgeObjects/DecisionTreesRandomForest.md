---
title: "Decision Trees/Random Forests"
description: "Decision Trees/Random Forests"
#lead: "AWS Kinesis"
keywords: 
    - decision trees
    - machine learning
    - supervised
contributors:
    - Andrew Cruez
date: 2022-03-01T00:00:00+00:00
lastmod: 2022-03-19T00:00:00+00:00
draft: false
toc: true
plotly: false
images: []
weight: 100
menu:
    docs:
        parent: "KnowledgeObjects"
---
## What are Decision Trees?
- Decision trees are a supervised machine learning method used for classification and regression. They are named after to the shape the chart takes

## Terminology
- Root Node - Node at the top of the tree which represents the entire sample or population of a data set.
- Splitting - Process of splitting a node into branches.
- Branches - A section of the tree representing the outcome of a test.
- Leaf/Terminal Node - A sub-node that does not split. 
- Internal/Decision Nodes - A sub-node that splits into further sub-nodes.
- Pruning - Removing sub-nodes of an internal/decision node. The opposite of splitting.
- Parent and child Node - A node divided into sub-nodes is a parent node, while the sub-nodes are child nodes.

## Concept
- Decision trees are a type of machine learning that uses "if this than that" type conditions to solve classification or regression questions. They are built by using a dataset with features we wish to examine in assigning a target value. For example, a dataset may contain patient data including chest pain, blood circulation, and blocked arteries, which we want to use to determine if a patient has heart disease. To determine which of the features in the data set will be the root node, we examine each feature individually to see which is the best indicator of our target value. If none of the features are 100% accurate in determining the target value, they are "impure" and we compare the impurity of each feature. There are different methods to evaluate impurity including:
- Estimate of Positive Correctness
- Gini Impurity
- Information Gain
- Variance Reduction
- Measure of Goodness
After the impurity evaluation method decides a root node, the rows assigned to each outcome are split into the child nodes, and the impurity process is repeated to determine which feature will be the next split for the node. This continues until all features are incorporated or until splitting a node doesn't result in a more accurate prediction/classification (child nodes would have higher impurity than parent node). Once the decision tree is complete, it can be used to predict or classify new data which doesn't already have an assigned target value.

## Random Forests
- A potential issue with decision trees is overfitting, or trees that are to strictly linked to the data used to create the tree, and will not be useful in predicting/classifying new data. 
- Random Forest is a collection of decision trees that are made up by taking subsets of features of the original dataset, and a subset of rows to create multiple decision trees that use up the entirety of the dataset, versus using the entirety of the dataset in one decision tree. With random forest each decision tree in the forest will create its own prediction/classification, and all results are aggregated into one final prediction/classification.

## How Do I Learn About It?
 - https://en.wikipedia.org/wiki/Decision_tree_learning
 - https://www.youtube.com/watch?v=7VeUPuFGJHk
 - https://towardsdatascience.com/decision-trees-and-random-forests-df0c3123f991
 - https://www.youtube.com/watch?v=LDRbO9a6XPU
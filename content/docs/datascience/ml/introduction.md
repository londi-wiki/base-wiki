---
weight: 999
title: "Introduction"
description: ""
icon: "article"
date: "2024-02-20T07:22:50+01:00"
lastmod: "2024-02-20T07:22:50+01:00"
draft: false
toc: true
katex: true
---

tags: regression, classification

# What is machine learning?

## Machine learning algorithmens

- Supervised learning
    - used most in real-world applications
- Unsupervised learning
- Recommender systems
- Reinforcement learning



## Supervised learning

> Learns form data **labeled** with the "right answers"

x -> y

input -> output label


Example:

email -> spam? (0/1)

> Regression
> Predict a number
> Infinitely many possible outputs


### Classification

> Shows the image a cat or a dog?

Classification: predict categories

Output: class or category

> Classification
> Predict categories
> small numbers of possible outputs

## Unsupervised learning

> Find something interesting in **unlabeled** data.

"clustering -algorithms"

- Clustering: Group similar data points together
- Anomaly detection: find unusual data points.
- Dimensionality reduction: Compress data using fewer numbers.


# Linear regression model

**House Prices**

| super script (i) | size in m2 | price |
|------------------|------------|-------|
| 1                | 1000       | 400   |
| 2                | 300        | 232   |


**Terminology**

- x = "input" variable / feature
- y = "output" variable / target variable

Example:

$(x^{(i)}, y^{(i)})$ = single training example

$(x^{(1)}, y^{(1)}) = (1000, 400)$

$(x^{(i)}, y^{(i)}) = i^{th} \text{ training example}$

> "i" is the index of the training set not the power of something.

x -> [f] -> y-hat

- x is called the input (or feature)
- function f is called the model
- The prediction of the y is called y-hat: $\hat{y}$ (or target)

Example: 

size -> [f] -> price (estimate)

## Represent f:

$f\substack{w,b}(x) = wx + b = y (not y-hat)$

w, b: parameters (or coefficients / weights)

> Often seen as f(x) = ...

This is called "linear regression with one variable or a single feature x". The exists also the expression "univariate linear regression".

## Cost function formula

> Squared error cost function

$\text{ Find w, b: } \hat{y}^{(i)} \text{ is close to } y^{(i)} \text{ for all } (x^{(i)}, y^{(i)})$

> We measure how far away the prediction is from target. 

$J(\substack{w,b}) = \frac{1}{2m} \sum_{i=1}^{m} ( \hat{y}^{(i)} - y^{(i)})^{2}$ the difference is called "error"

or:

$J(\substack{w,b}) = \frac{1}{2m} \sum_{i=1}^{m} ( f\substack{w,b}(x^{(i)}) - y^{(i)} )^{2}$

m = number of training examples





































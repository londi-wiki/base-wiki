---
weight: 999
title: "Formulas"
description: ""
icon: "article"
date: "2024-04-23T08:30:17+02:00"
lastmod: "2024-04-23T08:30:17+02:00"
draft: false
toc: true
---

# Notes

- What is ReLU (Rectified Linear Unit) in relation to Sigmoid function?
- 

# Step by step

1. Define the model
2. Specify loss and cost function
   1. Decide between e.g. BinaryCrossentropy, MeanSquaredError, ...
3. Gradient descent for every layer
   1. Compute derivatives for gradient descent using "backpropagation" `model.fit(X,y,epocs=100)`

## Activation functions

- Linear activation
  - for regression (y negative/positive)
- Sigmoid
  - for binary classification
- ReLU (Rectified Linear Unit)
  - for regression (y >= 0)
- Softmax

For hidden layers choose ReLU

```python
from tf.keras.layers import Dense
model = Sequential([
    Dense(units=25, activation='relu'), # hidden layer 1
    Dense(units=15, activation='relu'), # hidden layer 2
    Dense(units=1, activation='sigmoid'),  # output layer
])
```




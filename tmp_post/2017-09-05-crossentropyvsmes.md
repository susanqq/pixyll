---
layout:     post
title:      What is the different between MSE error and Cross-entropy error in NN
date:       2017-09-05
summary:    This blog summarized the difference between MSE vs Cross entroy as loss functions in NN
categories: jekyll pixyll
---
I find some useful blogs which discussed the difference of MSE vs. Cross Entropy. I want to summarize them from the theoretical and practical experience perspectives.
### Theoretical analysis:
Sigmoid +mse will converge slower compare sigmoid+cross entropy due to the gradient vanishing issue. 
See the derivation here:

Zhihu:[link](https://zhuanlan.zhihu.com/p/24693332)

Others:[link](http://neuralnetworksanddeeplearning.com/chap3.html)

Note: softmax can be considered in the sigmoid function family.

>!A paper also tries to analysis it:[link](http://books.jackon.me/Cross-Entropy-vs-Squared-Error-Training-a-Theoretical-and-Experimental-Comparison.pdf
)

### Practical understanding:

First, Cross-entropy (or softmax loss, but cross-entropy works better) is a better measure than MSE for classification, because the decision boundary in a classification task is large (in comparison with regression). MSE doesn't punish misclassifications enough but is the right loss for regression, where the distance between two values that can be predicted is small. 

Second, from a probabilistic point of view, the cross-entropy arises as the natural cost function to use if you have a sigmoid or softmax nonlinearity in the output layer of your network, and you want to maximize the likelihood of classifying the input data correctly. If instead you assume the target is continuous and normally distributed, and you maximize the likelihood of the output of the net under these assumptions, you get the MSE (combined with a linear output layer). For classification, cross-entropy tends to be more suitable than MSE -- the underlying assumptions just make more sense for this setting. That said, you can train a classifier with the MSE loss and it will probably work fine (although it does not play very nicely with the sigmoid/softmax nonlinearities, a linear output layer would be a better choice in that case). For regression problems, you would almost always use the MSE. Another alternative for classification is to use a margin loss, which basically amounts to putting a (linear) SVM on top of your network. 
ive for classification is to use a margin loss, which basically amounts to putting a (linear) SVM on top of your network.
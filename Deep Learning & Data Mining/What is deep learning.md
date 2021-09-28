---
tags : machine-learning/deep-learning
---

## Artificial Intelligence
The defination of artificial intelligence?
*the effort to automate intellectual tasks normally performed by humans*

**symbolic AI** : handcraft a sufficiently large set of explicit rules for manipulateing knowleges. After that, we have **expert systems**

## Machine Learning
Could a computer automatically learn these rules by looking at data?
*Turing test*

machine learning need : 
* Input data point
* Examples of the expected output
* Measure whether the algorithm is doing a good job

Examples : 
In task is speech recognition :
Data point might be sound files of speaking.
Output could be human-generated transcripts of sound files

Therefore the central problem is *meaningfully transform data*
machine learning is *searching for useful representations of some input data within a predefined space of possibilities, using guidance from feedback signal*

## Deep Learning
deep learning -> *layered representations learning* or *hierarchical representations learning*
compared to machine learning, sometimes we call machine learning *shallow learning*

layered representations are learned via *neural network* which is just a mathmetical framework

How it works?
* What a layer does : *weight*, the transformation implemented by a layer is parameterized by its weights
* *learning* means find a set of values for all weights , so that the input correctly map to their associated output

*Loss function* can measure how far this output from our expected.
And we can use the loss score to optimize the weights

### Brief Histroy
* 1958 : Perceptron
* 1969 : Perceptron has limitation
* 1980 : Multi-layer Perceptron
* 1986 : Backpropagation
* 1989 : 1 hidden layer is "good enough", why deep?
* 2006 : RBM Initialization
* 2009 : GPU
* 2011 : popular in speech recognition
* 2012 : win ILSVRC image competition

### Fully Connected Feedforward
![[Pasted image 20210126032146.png]]
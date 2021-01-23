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

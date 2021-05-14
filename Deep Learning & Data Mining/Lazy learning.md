## Lazy v.s. Eager leanring
* **Lazy** learning :
	* stores simple traning data, wait for sepicific test tuple
	* Less traning time, more predict time
	* multiple hypothesis from linear functions
* **Eager** leanring :
	* given traning set, build a model to classify new data
	* single hypothesis


## Instance-Based
Store training data and compare the new instance(data)
Methods:
* k-nearest neighbor approach
* locally weighted regression
* case-based reasoning

---
## KNN(K-Nearest Neighbor alg.)
* put instance in n-D space
* nearest neighbor defined by Euclidean distance

> k-NN return the most common value among the k training examples nearest to $X_q$

example:
	k = 8, there is 6 green & 2 red near black, so the black dot predict to green

>Given a test instance i, find the k closest neighbors and their labels
>Predict i’s label as the majority of the labels of the k nearest neighbors
---

## Case-Based reasoning
Need domain knowledge, Store symbolic description.
> Uses a database of problem solutions to solve new problems


---


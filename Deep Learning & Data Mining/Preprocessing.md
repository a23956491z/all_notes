---
tags : machine-learning
---

### Why Preprocessing?
Data in real situation is chaos
* **incomplete** or **noisy**: lacking attribute or make up the filling
    > eg., occupation="" , Salary="-10"
* **inconsistent**: discrepancy between duplicate records or attribute can't be cross validated

**MAJOR TASK**
* Data cleaning
* Data integration: integrating multiple dataset
* Data transformation: eg.normalization

---
### Descriptive Characteristics
**Central Tendency** :
* Mean, Weighted mean, Trimmed mean
* Median
* Mode: like the shape of data
    > eg. Unimodal, bimodal, trimodal

**Dispersion** :
* Quartile: *Q1(25th percentile), Q3(75th percentile)*
* Variance

**Boxplot(盒虛圖) Analysis**

* End line of box are **first & third quartiles**
* Middle line is the **median**
* Whisker is the used to mark the **minimum & maximum**
![Visualization of boxplay analysis](https://i.imgur.com/egYU84S.png)

**Normal Distribution Curve**
![Normal Distribution](https://i.imgur.com/Dv4MrhX.png)

**Histogram Analysis**
![Histogram](https://i.imgur.com/kZjB6Iz.png)

**Quantile-Quantile(Q-Q) Plot** : 
* Determining whether two data come from populations with common distribution.
* Plot of quantiles of first data set against the quantiles second data set
* Quantile : the fraction of points below the given value.
* Advantages :
	* The sample size do not need to be equal.
	* Many distributional aspects can be simultaneously tested.

![](https://www.itl.nist.gov/div898/handbook/eda/section3/gif/qqplot.gif)


**Scatter plot**

Present the relationship of two data
![Scatter plot](https://i.imgur.com/uABhVss.png)

* LOESS(Locally Weighted Scatterplot Smoothing) Curve:
add a smooth curve to a scatter plot to provide better perception of the pattern of dependence.
 	![Loess curve](https://i.imgur.com/hrbipis.png)
* Positively and Negatively Correlated
    ![Positively and Negatively Correlated](https://i.imgur.com/WnjvLGD.png)

---
### Data cleaning

**Deal Missing Data?**
* Ignore tuple: ignore when class label is missing
* Automatically Fill in :
	* Global constant e.g. new class "unknown"
	* Attribute mean
	* Most probable value by inference-based e.g. **Bayesian fomula** or **decision tree**

**What is Noisy Data**  :
Random error or variance in measured variable  

* similar but not noisy:  
    > duplicate records  
    > incomplete data  
    > inconsistent data  

**Binning Method** :  
* Equal-width(distance) partitioning :
Divide  the range in to N intervals of equal size(**uniform grid**)
e.g. bin 1 : A~B, bin 2 : B+1~C
	
* Equal-depth(frequency) partitioning :
Divide the range into N intervals, each containing same number of samples.

> eg.Sorted data for price (in dollars): 4, 8, 9, 15, 21, 21, 24, 25, 26, 28,
29, 34
> * Partition into equal-frequency (equi-depth) bins:
>    - Bin 1: 4, 8, 9, 15
>    - Bin 2: 21, 21, 24, 25
>    - Bin 3: 26, 28, 29, 34
> * Smoothing by bin means:
>    - Bin 1: 9, 9, 9, 9
>    - Bin 2: 23, 23, 23, 23
>    - Bin 3: 29, 29, 29, 29
> * Smoothing by bin boundaries:
>    - Bin 1: 4, 4, 4, 15
>    - Bin 2: 21, 21, 25, 25
>    - Bin 3: 26, 26, 26, 34


**Regression**
**Clustering**   
**Data discrepancy detection**  
* Use Metadata  

### Data intergration & transformation
Intergration: Combines data from sources in to a coherent store
* Schema intergraiton:  
> eg. A.cust-id ≡ B.cust-#  
* **Entity identification proble**:  
    To identify real world entities in different name  

**Handling Redundancy**  
* Object identification  
* Derivable data  
> *Redundant attributes may be able to be detected by
correlation analysis*  

**Correlation Analysis(for numerical data)**  
* Correlation coefficient(Pearson’s product moment coefficient)

**Data transformation**
* Smoothing: remove noise
* Aggreation: summarization
* Generalization: like hierarchy
* Normalization:
    * Min-max  
    $v' = \frac{v-min_{A}}{max_{A} - min_{A}}(new\_max_A-new\_min_A)+new\_min_A$
    * Z-svore  
    $v' = \frac{v-µ_A}{σ_A}$

    * Decimal Scaling  
    $v' = \frac{v}{10^j}$

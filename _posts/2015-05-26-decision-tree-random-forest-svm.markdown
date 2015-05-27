---
layout: post
title:  "A Closer Look at Decision Trees and Random Forests"
date:   2015-05-26 18:04:00
categories: jekyll update
---

## Decision Tree

#### 1. How Decision Tree Works

The definition of a decision tree (or classification & regression tree) procedure is:

*Beginning with a parent node which contains the entire sample, the C&RT procedure iteratively examines all available independent, or splitting, variables, selects the one that results in binary groups that are most different with respect to the dependent variable, according to a predetermined splitting criterion and stops when the stopping rule is satisfied. At the point that no further split is made, a terminal node is created.*[1]

**Splitting Criterion**

Node Impurity, or Diversity Index, denoted as $$Q_m(T)$$.

Improvement Measure of Node Impurity.

> Regression Tree

Squared-error Impurity: Sum of squared devitaions about the mean. 

The node predicts the sample mean of Y, which yields piecewise constant models. 

$$
Q_m(T) = \frac{1}{N_m}\sum_{x_i \in R_m}(y_i-\hat{c}_m)^2
$$

> Classification Tree

Define the proportion of class $$k$$ observations in node $$m$$.

$$
\hat{p}_{mk}
=\frac{1}{N_m}\sum_{x_i \in R_m}I(y_i=k)
$$

We classify the observations in node $$m$$ to class $$k(m)=argmax_k\hat{p}_{km}$$, the majority class in node $$m$$.

- Gini Index:

$$
Q_m(T)=\sum_{k\neq k'}\hat{p}_{mk}\hat{p}_{mk'}=\sum_{k=1}^K\hat{p}_{mk}(1-\hat{p}_{mk})
$$

- Misclassification Error:

$$
Q_m(T)=\frac{1}{N_m}\sum_{i\in R_m}I(y_i\neq k(m))=1-\hat{p}_{k(m),m}
$$

- Cross-entropy or Deviance:

$$
Q_m(T)=\sum_{k=1}^K\hat{p}_{mk}log\hat{p}_{mk}
$$

> Compute Improvement Measure

Take Gini Index as an example [1]

-- 1. The first step involves calculating Gini impurity function for the parent node, which is sometimes referred to as the Gini diversity index. (Diversity index)

-- 2. The second step involves calculating the Gini diver- sity index for each of the two child nodes into which the parent node splits. (diversity index1 and diversity index2)

-- 3. The third step involves calculating the weighted aver- age, according to the proportion of the parent node that is included in each child node, of the Gini diver- sity indexes for each of the child nodes. This can be obtained by solving the following equation:

Weighted diversity index = [(p1)(diversity index1)] + [(p2)(diversity index2)],

where p1 and p2 refer to the proportions of the parent node that are included in the respective child nodes.

-- 4. The last step requires calculating the Gini improve- ment measure, which is equal to the following:

Improvement measure = diversity index of parent node – weighted diversity index. 

Larger values of the Gini improvement measure indicate greater difference with respect to the prevalence of the depend- ent measure in the two child nodes. The independent variable whose split provides the largest value of the improvement measure is selected for splitting at each step.

> Illustrating Example

**Stopping Rule**

- Define the minimum number of individuals in the child node or in the terminal nodes

- Define the maximum number of levels to which the tree can grow.

- Predetermine the minimum value of the splitting criterion. 

#### 2. Related Algorithms [2]

> Classification Tree

The first published classification tree algorithm is **THAID**. Employing a measure of node impurity based on the distribution of the observed Y values in the node, THAID splits a node by exhaustively searching over all X and S for the split {X ∈ S} that minimizes the total impurity of its two child nodes. 

**C4.5** and **CART** are two later classification tree algorithms that follow this approach. C4.5 uses entropy for its impurity function, whereas CART uses a generalization of the binomial variance called the Gini index. 

Unlike THAID, however, they first grow an overly large tree and then prune it to a smaller size to minimize an estimate of the misclassi- fication error. CART employs 10-fold (default) cross- validation, whereass C4.5 uses a heuristic formula to estimate error rates. CART is implemented in the R system as RPART which we use in the examples below.

Building on an idea that originated in the **FACT** algorithm, **CRUISE**, **GUIDE** and **QUEST** use a two-step approach based on significance tests to split each node. **CHAID** uses significance tests and Bonferroni corrections to try to iteratively merge pairs of child nodes.

A comparision talbe is listed in [2].

> Regression Tree

Historically, the first regression tree algorithm is **AID** which appeared several years before THAID. The AID and CART regression tree methods follow Algorithm 1, with the node impurity being the sum of squared deviations about the mean and the node predicting the sample mean of Y.

**M5**, an adaptation of a regression tree al- gorithm by Quinlan uses a more computationally efficient strategy to construct piecewise linear models.

A comparision table of CART, GUIDE and M5 is listed in [2].


#### 3. Properties of Decision Tree (TBC)

- Deal with interactions among independent variables naturally. In the regression setting, it's hard to interpret interactions when there are more than 2 variables. 

- If X takes ordered values, the set S is an interval of the form (−∞, c]. Otherwise, S is a subset of the values taken by X. The process is applied recursively on the data in each child node. Splitting stops if the relative decrease in impurity is below a prespecified threshold.


## Random Forest


----
Wondering how I typed in the beautiful equations using Jekyll? These are two helpful posts that tell you how to use MathJex with Jekyll:

1. [MathJex](http://docs.mathjax.org/en/latest/start.html)
2. [MathJex with Jekyll](http://gastonsanchez.com/blog/opinion/2014/02/16/Mathjax-with-jekyll.html) 

Pandoc, on the other way, is a poweful tool to [use LaTex in Markdown](http://kesdev.com/you-got-latex-in-my-markdown/). 

----
References:

1. Lemon, Stephenie C., et al. "Classification and regression tree analysis in public health: methodological review and comparison with logistic regression." Annals of behavioral medicine 26.3 (2003): 172-181.

2. Loh, Wei‐Yin. "Classification and regression trees." Wiley Interdisciplinary Reviews: Data Mining and Knowledge Discovery 1.1 (2011): 14-23.


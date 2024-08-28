- A.I. (*sets of rules computer to follow*)
  - Machine Learning (*computer generate the rules based on input/output data*)
    - Neural Network / Deep Learning (*layers of ML*)

# Table of Content
- [Table of Content](#table-of-content)
- [Machine Learning:](#machine-learning)
- [Neural Nerwork:](#neural-nerwork)
  - [Learning](#learning)
  - [Intro(8/26/2024)](#intro8262024)
    - [Inductive vs Deductive](#inductive-vs-deductive)
      - [Supervised Learning (SL):](#supervised-learning-sl)
      - [Unsupervised Learning (UL):](#unsupervised-learning-ul)
      - [Reinforcement Learning (RL):](#reinforcement-learning-rl)
  - [Decision Trees (8/26/2024)](#decision-trees-8262024)
    - [Supervised Learning](#supervised-learning)
      - [Classification](#classification)
    - [Representations vs Algorithm](#representations-vs-algorithm)
      - [Decision Trees](#decision-trees)
      - [ID 3 Algorithm](#id-3-algorithm)
      - [Entropy](#entropy)
      - [Information Gain (IG)](#information-gain-ig)
      - [Bias](#bias)
  - [Regression (8/27/2024)](#regression-8272024)
      - [Error function](#error-function)
      - [Polynomial](#polynomial)
      - [Matrix Multiplication](#matrix-multiplication)
      - [Cross Validation](#cross-validation)
  - [Neural Network (8/27/2024)](#neural-network-8272024)
      - [Perceptron unit:](#perceptron-unit)
    - [Learning Rules:](#learning-rules)
      - [1. Perceptron learning rule](#1-perceptron-learning-rule)
      - [2. Gradient Descent](#2-gradient-descent)
    - [Sigmoid - Differentiable threshold](#sigmoid---differentiable-threshold)
    - [Back propagation](#back-propagation)
    - [local optimum](#local-optimum)
    - [Optimizing Weights](#optimizing-weights)
    - [Restriction Bias](#restriction-bias)
    - [Preference Bias](#preference-bias)



# Machine Learning: 
Generate **rules** for us based on data and answers, however, details of the rules are unclear.

    data + answer ==ML==> rules


# Neural Nerwork: 
Layers of data processes

```
  +--------------------------+
  | Input 1, Input 2 Input 3 |   Input Layer
  +--------------------------+
              v
              |<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<
              v                                           ^
  +-----------------------------+                         ^
  | Node 1, Node 2, Node 3, ... | Hidden Layer 1, 2, ...n ^
  +-----------------------------+                         ^
              v                                           ^
              |>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
              v
          +--------+
          | Answer |  Output Layer 
          +--------+
```
- **Input Layer**: Receives the input data features (e.g., pixels of an image, features of a dataset).
- **Hidden Layers**: Perform complex computations and feature extraction through activation functions. The number of hidden layers and the number of neurons in each layer are tunable parameters.
- **Output Layer**: Produces the final output (e.g., classification label, regression output).
- **Connections**: Each node in a layer is connected to nodes in the next layer through weighted connections, which are adjusted during training to minimize the error.

## Learning
- Task T
- Experience E
- Performance P
$$
  T\; \underset{\text{machine}}{\overset{\text{E}}{\xlongequal{\hspace{1cm}}>}}\;P\uparrow
$$

---

## Intro(8/26/2024)

### Inductive vs Deductive
  - inductive reasoning: from **instances/observations** to **generalizations**
    - He looks happy when drinking soup ===> the soup here is tasty
    - ML is bascially inductive generalization
  
  - deductive reasoning: from **general permises** to **specific conclusion**
    - Fish lives in water and Nemo is a fish ===> Nemo lives in water
    - 充分条件： if A => B is a *rule in the universe*, then B can be deducted from A



#### Supervised Learning (SL):
Functions approximation/induction from data with clear good or bad outcome (**bias**)

#### Unsupervised Learning (UL):
Description, Summarization, compressed/divided, no preset signal deciding the label (**unbias**)

**Example of utilizing both supervised and unsupervised learnings:**
  ```
    image pixels 
        | 
        | unsupervised learning
        V
    summaries
        | 
        | supervised learning
        V
      labels
  ```

#### Reinforcement Learning (RL):
In a series of bahaviors, only the final result is clearly stated (good/bad), but the process is not instructed.


**Optimization**:
  - Supervised: Labels data well
  - Reinforcement: behavior scroes well
  - Unsupervised: cluster scores well
  

---

## Decision Trees (8/26/2024)

### Supervised Learning
Classification vs Regression

#### Classification
True or False: if true, included, otherwise excluded for certain concept, could be binary or multiple classfications  

Terms: 
- **Instances**: set of inputs
- **Concept**: the mapping between objects and the membership in a set, the function/process that decide the output based on input, for classification the result is only True or false
- **Target [Concept]**: the answer that we want (the target function)
- **Hypothesis Class**: sets of concepts, here are the all classification concepts
- **Sample**: Training sets, inputs paired with label (credited output)
- **Candidate [Concept]**: a concept that might be the target concept
- **Testing**: Just like training sets, applying on candidate concept and see if candicate is accurate. Testing can't be the same as Sample.

### Representations vs Algorithm

#### Decision Trees

**A concept, a representation tool**

Decision 1: [Main question or decision]  
│  
├── Option A: [First option]  
│   │  
│   ├── Decision 2: [Follow-up question or decision for Option A]  
│   │   │  
│   │   ├── Option A1: [First option for Decision 2]  
│   │   │   ├── Outcome A1a: [Result of choosing Option A1]  
│   │   │   └── Outcome A1b: [Alternative result of choosing Option A1]  
│   │   │  
│   │   └── Option A2: [Second option for Decision 2]  
│   │       ├── Outcome A2a: [Result of choosing Option A2]  
│   │       └── Outcome A2b: [Alternative result of choosing Option A2]  
│   │  
│   └── Outcome A: [Direct outcome of choosing Option A]  
│
└── Outcome B: [Direct outcome of choosing Option B]  

1. Pick best attribute
2. Asked question 
     - attribute with discrete options won't show up again along the tree because it gives no information gain whatsoever
     - **for continous attribute (like age), same attribute can show up again along the tree with different question**
3. Follow the answer path
4. stop if
     - everything classified correctly
     - no more attributes
     - no overfitting (good classification but bad generalization)
       - cross-validation
       - pruning
5. go to 1 


--

N attributes:
- N-OR: function ANY, linear number of nodes (N)
- N-XOR: function if ODD PARITY (true if number of true attributes is odd), exponential number of nodes (2^N)

#### ID 3 Algorithm
A top-down learning algorithm

loop: 
- find best attribute: A
- assign A as decision attribute for Node
- for each value of A, create a descendant of node
- sort training examples of leaves
- if examples perfectly classified, stop
- else, iterate over leaves
  
--

#### Entropy
measures the amount of **uncertainty** or surprise associated with a random variable or the amount of information required to describe the random variable’s possible outcomes.

The entropy $H(S)$ of a random variable $S$ is given by:

$$
H(S) = - \sum_{i=1}^{n} p(s_i) \log_2 p(s_i)
$$

where:

- $H(S)$ is the entropy of the random variable $S$.
- $p(s_i)$ is the probability of occurrence of each possible value $s_i$ of $S$.
- The summation is over all possible values of $S$.
- $\log_2$ denotes the logarithm to the base 2.

--

#### Information Gain (IG)
a key concept measures the effectiveness of an attribute in classifying a dataset. 

The reduction in entropy or surprise by transforming a dataset and is used to determine which feature to split on at each step in building the decision tree. 

The IG for an attribute $A$ when splitting a dataset $S$ is the reduction in entropy after the dataset is split on attribute $A$.

$$
IG(S, A) = H(S) - \sum_{v \in \text{Values}(A)} \frac{|S_v|}{|S|} H(S_v)
$$

where:
- $IG(S, A)$: Information Gain of attribute $A$ relative to dataset $S$.
- $H(S)$: Entropy of the original dataset $S$.
- $\text{Values}(A)$: Set of all possible values of attribute $A$.
- $S_v$: Subset of $S$ where attribute $A$ has value $v$.
- $\frac{|S_v|}{|S|}$: Proportion of dataset $S$ that takes the value $v$ for attribute $A$.
- $H(S_v)$: Entropy of the subset $S_v$.

--

#### Bias
Two kinds of bias:
  - **Restriction bias**: the hypothesis set (all possible hypothesis that generalized from training data)
  - **Preference bias** (inductive bias): $h \in \mathbb{H}$, 
    - good split at the top
    - correct over incorrect
    - shorter tree over longer tree (ID 3 preferred)

---

## Regression (8/27/2024)
mapping **scalar($x / y$) or vector($\vec{x}/\vec{y}$)** inputs to outputs;

**regress**: return to a former or less developed state, but **regression** in math doesn't match its original meaning anymore.

--

#### Error function
The error function (also known as the cost or loss function) in regression, often represented as the **Mean Squared Error** (MSE), is given by:

$$
\text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2
$$

where:

- $y_i$ is the actual value.
- $\hat{y}_i$ is the predicted value.
- $n$ is the number of data points.


**Error sources**:
- sensor error
- maliciously - being given bad data
- trasncription - human error
- unmodeled influence

--

#### Polynomial
The formula for a polynomial regression model of degree $m$ is given by:

$$
\hat{y}_i = \beta_0 + \beta_1 x_i + \beta_2 x_i^2 + \beta_3 x_i^3 + \ldots + \beta_m x_i^m
$$

where:

-	 $\hat{y}_i$  is the predicted value for the i-th data point.
-	 $x_i$  is the input feature for the i-th data point.
-	 $\beta_0$, $\beta_1$, $\beta_2$, $\ldots$, $\beta_m$ are the coefficients of the polynomial model.
-	 $m$  is the degree of the polynomial, which determines the highest power of $x_i$.

--

#### Matrix Multiplication

Matrix  A  is of size  $m \times n$ :

$$
A =
  \overbrace{
    \begin{bmatrix}
      a_{11} & a_{12} & \ldots & a_{1n} \\
      a_{21} & a_{22} & \ldots & a_{2n} \\
      \vdots & \vdots & \ddots & \vdots \\
      a_{m1} & a_{m2} & \ldots & a_{mn}
    \end{bmatrix}
  }^n
  \left.
  \right\}m
$$

Matrix  B  is of size  $n \times p$ :

$$
B =
  \overbrace{
    \begin{bmatrix}
      b_{11} & b_{12} & \cdots & b_{1p} \\
      b_{21} & b_{22} & \cdots & b_{2p} \\
      \vdots & \vdots & \ddots & \vdots \\
      b_{n1} & b_{n2} & \cdots & b_{np}
    \end{bmatrix}
  }^p
  \left.
  \right\}n
$$

Then the product  $C = A \cdot B$  will be a matrix of size  $m \times p$ , where:

$$
  C =
  \begin{bmatrix}
    a_{11} & a_{12} & \ldots & a_{1n} \\
    a_{21} & a_{22} & \ldots & a_{2n} \\
    \vdots & \vdots & \ddots & \vdots \\
    a_{m1} & a_{m2} & \ldots & a_{mn}
  \end{bmatrix} 
  \times
  \begin{bmatrix}
    b_{11} & b_{12} & \cdots & b_{1p} \\
    b_{21} & b_{22} & \cdots & b_{2p} \\
    \vdots & \vdots & \ddots & \vdots \\
    b_{n1} & b_{n2} & \cdots & b_{np} \\
  \end{bmatrix}
  \\=
  \begin{bmatrix}
    c_{11} & c_{12} & \cdots & c_{1p} \\
    c_{21} & c_{22} & \cdots & c_{2p} \\
    \vdots & \vdots & \ddots & \vdots \\
    c_{m1} & c_{m2} & \cdots & c_{mp}
  \end{bmatrix}
$$

The elements of matrix $C$  are computed as:

$$
  c_{ij} = \sum_{k=1}^{n} a_{ik} \cdot b_{kj}
$$

where:

-	$c_{ij}$  is the element in the i-th row and j-th column of the resulting matrix $C$ .
-	$a_{ik}$  is the element in the i-th row and k-th column of matrix $A$ .
-	$b_{kj}$  is the element in the k-th row and j-th column of matrix $B$ .
-	The summation  $\sum_{k=1}^{n}$  represents the dot product of the i-th row of matrix $A$ and the j-th column of matrix $B$.

--

#### Cross Validation
Take part of the training set and use it as trial test set.

e.g., For each model, and assuming training data is seperated into **4 folds** (set of data)
  - Train on **3 folds** and use the last fold as **trial test set**, do this for each combination
  - get all the errors from trial test set and average the error
  - Pick the model with the lowest average error

Very powerful when trying to decide the freedom of polynomial model, 
  - **less freedom** -> **underfitting**
  - **more freedom** -> **overfitting**.

---

## Neural Network (8/27/2024)
 
#### Perceptron unit: 

A tool for binary **classification** (vs regression)

A perceptron receives multiple input signals, applies **weights** to them, **sums** them up, adds a **bias**, and then applies an **activation function** (typically a step function) to determine the output. The perceptron model can be described mathematically as follows:

**Perceptron Formula**

Given:

-	Inputs:  $x_1, x_2, \ldots, x_n$
-	Weights:  $w_1, w_2, \ldots, w_n$ 
-	Bias:  $b$ 
-	Activation function:  $f(z)$  (commonly a step function or a sign function)

The output  $y$  of the perceptron can be defined by the following formulas:

1.	Weighted Sum Calculation:

$$z = sum_{i=1}^{n} w_i x_i + b = w_1 x_1 + w_2 x_2 + \ldots + w_n x_n + b$$

2.	Output Calculation using Activation Function:

$$y = f(z) = f\left( \sum_{i=1}^{n} w_i x_i + b \right)$$


Where the activation function  f(z)  is typically a step function defined as:

$$
f(z) =
\begin{cases}
1 & \text{if } z \geq 0 \\
0 & \text{if } z < 0
\end{cases}
$$

or a sign function for binary outputs:

$$
f(z) =
\begin{cases}
1 & \text{if } z \geq 0 \\
-1 & \text{if } z < 0
\end{cases}
$$

--

### Learning Rules:

#### 1. Perceptron learning rule

The perceptron rule iteratively updates the weights of the perceptron based on the error between the predicted output and the actual output for each training example. The learning process continues until the perceptron correctly classifies all training examples or reaches a predefined number of iterations.

 - Great for classifying data set that is **Linearly Separable**

**Perceptron Update Rule Formula**

Given:

-	Inputs:  $x_1, x_2, \ldots, x_n$  (features of the training example)
-	Weights:  $w_1, w_2, \ldots, w_n$  (weights corresponding to each input)
-	Bias:  $b$  (bias term)
-	Learning rate:  $\eta$  (a small positive number, typically less than 1)
-	Actual output:  $y$  (target label, usually 1 or -1 for binary classification)
-	Predicted output:  $\hat{y}$  (output of the perceptron after applying the activation function)

The perceptron output  $\hat{y}$  is calculated as:

$$
\hat{y} = f(z) = f\left( \sum_{i=1}^{n} w_i x_i + b \right)
$$

where  $f(z)$  is the activation function (typically the sign function for binary classification):

$$
f(z) =
\begin{cases}
1 & \text{if } z \geq 0 \\
-1 & \text{if } z < 0
\end{cases}
$$

The perceptron update rule for each weight $w_i$  and bias  $b$  is:

$$
w_i \leftarrow w_i + \eta \cdot (y - \hat{y}) \cdot x_i \quad \text{for all } i = 1, 2, \ldots, n
$$

$$
b \leftarrow b + \eta \cdot (y - \hat{y})
$$

Explanation of the Update Rule

-	Error Calculation:  $(y - \hat{y})$  represents the error term, which is the difference between the actual output  $y$  and the predicted output  $\hat{y}$ .
-	If  $y = \hat{y}$ , the perceptron has correctly classified the input, and no update is necessary.
-	If  $y \neq \hat{y}$ , the weights are adjusted to reduce this error in future iterations.
-	Learning Rate:  $\eta$  is the learning rate that controls the magnitude of the weight updates. A smaller learning rate results in smaller updates and more gradual convergence.
-	Weight Update: Each weight  $w_i$  is updated by adding a fraction of the error multiplied by the corresponding input  $x_i$ . This ensures that the weights are adjusted in the direction that minimizes the error.
-	Bias Update: The bias  $b$  is updated similarly to the weights, using the error term.

Perceptron Learning Algorithm

1.	Initialize the weights  $w_i$  and bias  $b$  to small random values (or zeros).
2.	For each training example  $(x, y)$ :
•	Compute the predicted output  $\hat{y} = f(z)  where  z = \sum_{i=1}^{n} w_i x_i + b$ .
•	Update each weight  $w_i$  using the perceptron update rule.
•	Update the bias  $b$  using the perceptron update rule.
3.	Repeat steps 2 until the perceptron correctly classifies all training examples or a predefined number of iterations is reached.

--

#### 2. Gradient Descent 
- for finding data set that is **Non-Linearly Separable**
  
Gradient Descent is an iterative optimization algorithm used for finding the minimum of a function. In the context of machine learning, it is used to minimize the cost function  $J(\theta)$ , which measures the difference between the predicted values and the actual values of the target variable.

The algorithm works by taking small steps in the direction of the negative gradient (the direction of the steepest descent) of the cost function with respect to the model parameters. Each step updates the parameters to reduce the cost function value.

**Gradient Descent Formula**

Given a cost function  $J(\theta)$ , where  $\theta$  represents the parameters of the model (e.g., weights in linear regression or coefficients in logistic regression), the update rule for gradient descent is:

$$
\theta := \theta - \eta \cdot \nabla J(\theta)
$$

where:

-	$\theta$  is the parameter vector (e.g., weights in a linear model).
-	$\eta$  is the learning rate, a small positive value that controls the step size of each iteration.
-	$\nabla J(\theta)$  is the gradient of the cost function  $J(\theta)$  with respect to the parameters  $\theta$ . This gradient is a vector of partial derivatives:

$$
\nabla J(\theta) = \left[ \frac{\partial J(\theta)}{\partial \theta_1}, \frac{\partial J(\theta)}{\partial \theta_2}, \ldots, \frac{\partial J(\theta)}{\partial \theta_n} \right]
$$

Steps in Gradient Descent

1.	Initialize the parameters  $\theta$  with some values (often zeros or small random numbers).
2.	Compute the Cost Function  $J(\theta)$  using the current parameter values.
3.	Compute the Gradient  $\nabla J(\theta)$  of the cost function with respect to each parameter.
4.	Update the Parameters: Adjust each parameter  $\theta_j$  by subtracting the product of the learning rate  $\eta$  and the partial derivative of the cost function with respect to that parameter:

$$
\theta_j := \theta_j - \eta \cdot \frac{\partial J(\theta)}{\partial \theta_j}
$$
5.	Repeat steps 2-4 until the cost function converges to a minimum or a predefined number of iterations is reached.

Types of Gradient Descent

-	Batch Gradient Descent: Computes the gradient using the entire training dataset. This is computationally expensive for large datasets but provides a smooth convergence path.
-	Stochastic Gradient Descent (SGD): Computes the gradient using a single training example at each iteration. It is much faster and can handle large datasets but introduces more noise, leading to a less smooth convergence path.
-	Mini-Batch Gradient Descent: A compromise between Batch Gradient Descent and SGD. It computes the gradient using a small subset (mini-batch) of the training data. This approach balances the convergence speed and noise reduction.

--

### Sigmoid - Differentiable threshold

The sigmoid function, also known as the logistic function, is defined mathematically as:

$$
\sigma(z) = \frac{1}{1 + e^{-z}}
$$

where:

-	 $\sigma(z)$  is the sigmoid function applied to the input  $z$ .
-	 $z$  is a real-valued input, which could be the weighted sum of inputs in a neural network or the linear combination of features in logistic regression.
-	 $e$  is the base of the natural logarithm, approximately equal to 2.71828.

Properties of the Sigmoid Function

1.	Range: The output of the sigmoid function is always between 0 and 1:
$$
0 < \sigma(z) < 1
$$
2.	Shape: The sigmoid function has an “S”-shaped curve. It is:
	-	Monotonic: It is a strictly increasing function.
	-	Bounded: It has horizontal asymptotes at  $y = 0$  and  $y = 1$ .
3.	Derivative: The derivative of the sigmoid function is useful in optimization and backpropagation in neural networks. The derivative is given by:
$$
\sigma{\prime}(z) = \sigma(z) \cdot (1 - \sigma(z))
$$
This property simplifies gradient calculations in neural networks.

--

### Back propagation
### local optimum
### Optimizing Weights
### Restriction Bias
### Preference Bias
Algorithm's selection of one representation over another

What algorigthm? 
  - Gradient descent
  - Initial weights -> small random values
    - variability -> avoid local minimal
    - low complexity -> simpler explanations
    - better generalization error ($Occam's Razor: entities\;should\;not\;be\;multiplied\;unnecessarily.$)

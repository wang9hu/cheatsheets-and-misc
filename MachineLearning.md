- A.I. (*sets of rules computer to follow*)
  - Machine Learning (*computer generate the rules based on input/output data*)
    - Neural Network / Deep Learning (*layers of ML*)

# Table of Content
- [Table of Content](#table-of-content)
  - [Machine Learning (ML) vs Neural Network(NN)](#machine-learning-ml-vs-neural-networknn)
    - [ML](#ml)
    - [NN](#nn)
  - [Learning from TextBook](#learning-from-textbook)
    - [Design a learning system for checker game:](#design-a-learning-system-for-checker-game)
      - [1. Choose the E (what data ML want to learn from)](#1-choose-the-e-what-data-ml-want-to-learn-from)
      - [2. Choose the Target Function (what ML want to get from learning)](#2-choose-the-target-function-what-ml-want-to-get-from-learning)
      - [3. Choose the representation for the Target Function (what would the Rep Func look like)](#3-choose-the-representation-for-the-target-function-what-would-the-rep-func-look-like)
      - [4. Choose a Function approximation Algorithm (how to learn)](#4-choose-a-function-approximation-algorithm-how-to-learn)
      - [5 The Final Design](#5-the-final-design)
    - [Decision Tree Learning](#decision-tree-learning)
        - [Decision tree is basically the **representation function**.](#decision-tree-is-basically-the-representation-function)
        - [Classification problems (targe problems for decision tree)](#classification-problems-targe-problems-for-decision-tree)
      - [ID 3 algorithm, the basic decision tree algorithm](#id-3-algorithm-the-basic-decision-tree-algorithm)
      - [Best Classifier](#best-classifier)
      - [ID3's Characteristics](#id3s-characteristics)
      - [Inductive Bias in decision tree learning](#inductive-bias-in-decision-tree-learning)
      - [Avoid Overfitting](#avoid-overfitting)
        - [Reasons for this to happen:](#reasons-for-this-to-happen)
        - [Approaches to avoid:](#approaches-to-avoid)
    - [Neural Networks](#neural-networks)
      - [Perceptrons](#perceptrons)
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
  - [Instance Based Learning (9/4/2024)](#instance-based-learning-942024)
    - [K-Nearest Neighbors algorithm (K-NN)](#k-nearest-neighbors-algorithm-k-nn)
      - [Distance measurement](#distance-measurement)
      - [K-NN Bias](#k-nn-bias)
    - [Curse of Dimensionality](#curse-of-dimensionality)
  - [Ensemble Learning Boosting (9/4/2024)](#ensemble-learning-boosting-942024)
    - [Ensemble Learning Algorithms](#ensemble-learning-algorithms)
    - [Ensumble Boosting](#ensumble-boosting)
      - ["hardest" examples:](#hardest-examples)
      - ["weak" learning algorithm ('weak' learner):](#weak-learning-algorithm-weak-learner)
      - [Adaboost](#adaboost)
        - [Note **weight** can be for anything, the training data, the hypothesis or the parameter in hypothesis.](#note-weight-can-be-for-anything-the-training-data-the-hypothesis-or-the-parameter-in-hypothesis)
  - [Kernel Methods \& SVMs (9/10/2024)](#kernel-methods--svms-9102024)
    - [Support Vector Machines (SVM)](#support-vector-machines-svm)



## Machine Learning (ML) vs Neural Network(NN)
### ML
Generate **rules** for us based on data and answers, however, details of the rules are unclear.

    data + answer ==ML==> rules


### NN
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

## Learning from TextBook

- Task T
- Training Experience E
- Performance P
  
$$
    T\;\underset{\underbrace{\text{machine learning}}_{\underset{\text{Target Function}}{\dArr}}}{\overset{\text{E}}{\xlongequal{\hspace{2cm}}>}}\;P\uparrow
$$
### Design a learning system for checker game:
#### 1. Choose the E (what data ML want to learn from)

Attributes of E:
- Types of feedback: direct vs indirect
  - Early decision had indirect impact on the final result, so credit assignment is hard because both early moves and later moves can affect the final results.
  - Direct training feedback (correct for each move) is easier to train with than indirect feedback.
- Degree of control
  - learn from pre-selective information 
  - self-proposed info with guidence 
  - no teacher 
  - ....
- Representation distribution level of training data vs test examples (real-world senario)

e.g., For checker, E is mostly indirect except for end game board state.

#### 2. Choose the Target Function (what ML want to get from learning)
Setup a output that is efficiently computable for measuring performance, reduce the problem to **an operational description of the ideal target function $V$**.

Learning algorithms can only acquire some approximation ($\hat{V}$) to the target function, so this step is also called **function approximation**.

e.g., 
$$
  V:B \rarr \mathbb{R}
$$
- $B$ is a set of all legal board state
- mapping any legal board state from the set $B$ to some real value 

#### 3. Choose the representation for the Target Function (what would the Rep Func look like)
Find the representation (description) of the function ($\hat{V}$) that the learning program will use. 

**Tradoffs**: the more expressiveness: the closer to target function($V$), but also need more training data

e.g., representation function for checker game:
$$
  \hat{V}(b) = w_{0} + w_{1}x_{1} + w_{2}x_{2} + w_{3}x_{3} + w_{4}x_{4} + w_{5}x_{5} + w_{6}x_{6}
$$
- $\hat{V}(b)$ is the represent value
- $x_{1}$: the number of black pieces on the board 
- $x_{2}$: the number of red pieces on the board
- $x_{3}$: the number of black kings on the board 0 
- $x_{4}$: the number of red kings on the board
- $x_{5}$: the number of black pieces threatened by red (i.e., which can be captured on red's next turn)
- $x_{6}$: the number of red pieces threatened by black
- $w_{0}$ to $w_{6}$ are numerical coefficients, or weights, to determine the impotance of each feature

#### 4. Choose a Function approximation Algorithm (how to learn)
- **Estimate training values**
  e.g. for borad game, the $E$ is indirect, so a rule for estimating training values is below: 
  $$
    V_{train}(b)\;\larr\;\hat{V}(Successor(b))
  $$
  - $\substack{V}{train}(b)$ is any intermediate board state's training value.
  - $\hat{V}(Successor(b))$ is the next board state's representation function value.
  - The end game state is either 0 or 100 (loss or win), values are arbitary. 
- **Adjust the weights**
  specify learning algorithm for any training examples $\{ <b,{V}_{train}(b)> \}$.
  e.g., one common approach is to define the best hypothesis (combination of weights) by minimizing the squared error E
  $$
    E \equiv\underset{<b,\;V_{train}(b)> \;\subseteq{\text{ training examples}}}{\sum}(V_{train}(b)-\hat{V}{b})^{2}
  $$

  - **Least mean squares** (LMS) is known for finding weights of a linear function that minimize $E$ based on gradient descent. For each training example $\{ <b,\;\substack{V}{train}(b)> \}$:
      - use current weigths to calculate $\hat{V}(b)$
      - for each weigth $w_{i}$, update it as
        $$
            w_{i} \larr w_{i} + \eta\;(V_{train}(b) - \hat{V}(b))\;x_{i}
        $$
          - $\eta$ is a small constant (e.g., 0.1) that moderates the size of the weight update.
      - update happends after each training example (data instance), which is called **stochastic gradient descent**.
      - data order matters for this algorithm, so usually use the same set of data to train multiple times or use crose-validation to get more reliable estimate.
  
#### 5 The Final Design
  Iterate over 4 distinct program modules: Many machine learning systems can-beusefully characterized in terms of these four generic modules.
  ```
    Performance       
      System       >>> Solution trace (game history) >>>    Critic

         ^                                                    v
         ^                                                    v
     New Problem                                         Training examples
 (initial game board)                  (<b_1, V_train(b_1)>, <b_2, V_train(b_12)>, ...)
         ^                                                    v  
         ^                                                    v
         ^                                                    v
                             
    Experiment      <<<<<< Hypothesis (V_hat) <<<<<<<      Generalizer
     Generator
  ```

  - The **Performance System**: Solve the given performance task.
    - for checker game: given a new game as input, use $\hat{V}$ to evaluate a trace of its solution (game history) as output.
  - The **Critic**: Takes the inputs $\{b_{1}, b_{2}, ...\}$ and produces a set of training examples  $\{<b_{1},{V}_{train}(b_{1})>, <b_{2},{V}_{train}(b_{2})>, ... \}$ of the target functions .
    - for checker game: takes game history and produces the estimate $V_{train}$ according to the successor rule defined before
  - The **Generalizer**: takes the training examples as input and produces an output hypothesis that is estimate of the target function.
    - for checker game: the generalizer corresponds to the LMS algorithm and the output hypothesis is the function $\hat{V}$ described by learned weightes $w_{0}, w_{1}, ...$
  - The **Experiment Generator**: takes the current hypothesis from generalizer and produces a new problem for the **Performance System** to explore, following certain stragegy.
    - for checker game: use the new hypothesis to generate a new game start from initial game board, each step using the optimal move.
  
### Decision Tree Learning
A method for approximating discrete-valued functions that is *robust to noisy data* and capable of learning disjunctive expressions.

##### Decision tree is basically the **representation function**.
```
                  [Feature 1]
                /             \
              A1                A2
              |                  |
          [Feature 2]         [Feature 3]
        /     |     \           /      \
       B1     B2    B3         C1       C2
       |      |      |         |        |
   ActionX ActionY ActionZ  ActionY  ActionX
```
##### Classification problems (targe problems for decision tree)
  - Instances are represented by **attribute-value pairs**
  - The target function has **discrete output** values (not necessarily binary)
  - *Disjunctive descriptions may be required.*
  - *The training data may **contain errors** or may contain **missing attribute** values*


#### ID 3 algorithm, the basic decision tree algorithm
Construct the tree top-down using $ID3(Examples,\;Target\_attribute,\;Attributes)$ algorithm:

  - create a $Root$ node
    - if all examples are the same, return the $Root$ node with lable = that value
    - if no more target attribute, return the $Root$ node with label = the most common value of the target attribute
    - otherwise
      - From $Target\_attributes$, find the attribute $A$ that best classifies $Examples$
      - Use $A$ as the dicision attribute for $Root$
      - For each possible value, $v_{i}$ of $A$
        - Add a new tree branch below $Root$, corresponding to $A=v_{i}$
        - Let $Examples_{A:v_{i}}$ be subset of Examples that have $v_{i}$ for $A$
          - If $Examples_{A:v_{i}}$ is empty, then add a leaf node with label = most common value of $Target\_attribute$ in $Example$
          - Else below this new branch add the subtree $ID3(Examples_{A:v_{i}},\;Target\_attribute,\;Attributes - {A})$

#### Best Classifier

- ##### Entropy measures the homogeneity of *Examples*:
  Entropy is a measure of the expected encoding length measured in bits, if the 
  $$
  Entropy(S) = - \sum_{i=1}^{n} p_{s_i} \log_2 p_{s_i}
  $$
  - Maximum Entropy is $\log_2 k$, where k is the number of classes and all classes are equally likely.
    - For **boolean classification** (true or false), $0 \le Entropy\le1$.
  - Minimum Entropy is 0, where one class has a probability of 1 and others have a probability of 0.

- ##### Information Gain (IG)
  IG is the reduction in entropy caused by partitioning the examples according to attribute $A$.
  $$
  IG(S, A) = Entropy(S) - \sum_{v \in \text{Values}(A)} \frac{|S_v|}{|S|} Entropy(S_v)
  $$
  The **larger** the IG, the **better the attribute** for classifying current trainig examples.


#### ID3's Characteristics
- Pros:
  - Simplicity
  - Efficiency
  - Interpretability
- Cons:
  - Local optimal solution over global optimal solution due to its simple-to-complex, hill-climbing search through
  - Overfitting (pruning methods can mitigate this)
  - Continous attributes require preprocessing techniques


#### Inductive Bias in decision tree learning
- **Only** preference bias (search strategy bias)
  - solely a consequence of the ordering of hypotheses
- **No** representation bias (hypothesis space bias)
  - the hypothesis space is complete (*search from finite discrete-valued hypothesis*)

#### Avoid Overfitting
Hypothesis that fits the training examples better over the entire distribution of instance

##### Reasons for this to happen:
- there is noise in the data 
- training examples is too small or not representative enough
  
##### Approaches to avoid:
- Stop growing the tree earlier, but hard to know when
- Overfit the data and then post-prune (**preferred**)
  - **reduced-error pruning**


### Neural Networks
Target problem for NN:
- Instances are attribute-value pairs
- Target function output may be **scalar** or **vector** of scalars
- Training examples may contain errors
- Long trainig times are acceptable
- Fast evaluation of the learned target function may be required
- Not necessarily human understandable

#### Perceptrons


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
├── Option A: [First option]  
│   ├── Decision 2: [Follow-up question or decision for Option A]  
│   │   ├── Option A1: [First option for Decision 2]  
│   │   │   ├── Outcome A1a: [Result of choosing Option A1]  
│   │   │   └── Outcome A1b: [Alternative result of choosing Option A1]  
│   │   └── Option A2: [Second option for Decision 2]  
│   │       ├── Outcome A2a: [Result of choosing Option A2]  
│   │       └── Outcome A2b: [Alternative result of choosing Option A2]  
│   └── Outcome A: [Direct outcome of choosing Option A]  
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
1. find best attribute: A
2. assign A as decision attribute for Node
3. for each value of A, create a descendant of node
4. sort training examples of leaves
5. if examples perfectly classified, stop
6. else, iterate over leaves
  
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
  - **Restriction bias**: the hypothesis set, or weight set (all possible hypothesis that generalized from training data)
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
-	Bias:  $b$  (bias term) or $w_0$ while $x_0 = 1$
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
•	Compute the predicted output  $\hat{y} = f(z)$  where  $z = \sum_{i=1}^{n} w_i x_i + b$ .
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

The sigmoid function, also known as a special case of logistic function, is defined mathematically as:

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


---

## Instance Based Learning (9/4/2024)
Take all data and put them in the database, and search over database when query

Problem:
- no generalization 
- High chance of overfitting
- Same data input might have different data output

Solution:
- find the $K$ nearest neighbors (distance = similarity)

### K-Nearest Neighbors algorithm (K-NN)
**Lazy learner**

**Can be used for both classification and regression**

Given: 
- Training Data $D = \{x_i, y_i\}$ 
- Query point $q$
- Distance metric: $d(q,x)$  (domain knowledge)
- Number of Neighbors $K$

Find:
- $NN=\{i: d(q, x_i) \text{ K smallest}\}$
- return 
  - classification: vote (weighted, plurity)
  - regression: mean (weighted)

Tradeoff comparing K-NN (lazy learner) to linear regression (eager learner):
- learning time: 
  - K-NN: $O(1)$
  - linear regression: $O(n)$
- query time:
  - K-NN: $O(lgn + K)$
  - linear regression: $O(1)$

#### Distance measurement
**Choice of distance function really matter**

$d(x, q)$
- **Euclidean** (weighted or not): $d(\mathbf{x_q}, \mathbf{x_i}) = \sqrt{(x_{q_{1}} - x_{i_{1}})^2 + (x_{q_{2}} - x_{i_{2}})^2 + \ldots + (x_{q_{n}} - x_{i_{n}})^2}$
- **Manhattan** (weighted or not): $d=\min{\sum{\{up, down, left, right\}}}$
- **Locally weighted regression**: only use near $K$ points for the regression

#### K-NN Bias
Preference Bias: **perferred bias we choose to believe that is true**

- Similarity
  - Locality -> near points are similar
  - Smootheness -> averaging
- All freatures matter equally ($x_1,x_2,...$)
  - for $y=x_1^2 + x_2$, $x_1$ and $x_2$ are treated equally

### Curse of Dimensionality
As the number of **features or dimensions grows**, the amount of data we need to *generalize accurately* also **grow exponentially**.

## Ensemble Learning Boosting (9/4/2024)
Combine simples rules together to create a more complex rule that works better than simple rules.
### Ensemble Learning Algorithms
From training examples:

- **Bagging** (or bootstrap aggregation):
  - Learn over a subset of examples -> rule 1
  - Learn over another subset of examples -> rule 2
  - ...
  - all rules are independent -> averaging the output of all rules

  e.g., use uniformly random subsets and average the regressions, 

- **Boosting**:
  1. use a subset of examples => model 1
  2. use model 1 to test all training examples => poorly behaved examples ("hardest")
  3. use hardest examples => model 2 
  4. combine model 1 and 2 => model 3  
  5. go to step 2 until m cycles

### Ensumble Boosting
Instead of pick subset randomly, use hardest examples (doesn't fit for current hypothesis) and use weighted mean.

e.g.,
Error:
$$
  Pr_\mathbb{D:x}[h(x)\neq c(x)]
$$
- $Pr$ is the probability
- $\mathbb{D}$ is the example set distribution, $\sum\mathbb{D(i)} = 1$, e.g., for uniformly distributed discrete $n$ examples, $\mathbb{D}(i)=1/n$
- $x$ is the example instance
- $h$ is the candidate hypothesis 
- $c$ is the target hypothesis
  
for classification, 
- Error: number of mismatch
- Error rate:  number of mismatch over total number of examples
  - **Implicit idea:** saying all examples are equally as important, or having the same probability of showing up

#### "hardest" examples:
Examples that have less probability to show up in the example set
  - weigthed mean

#### "weak" learning algorithm ('weak' learner):
A weak learning is the algorithm that tries to find a model that can perfrom slightly better than random hypothesis (just above 50% in terms of the **weighted** examples).

- Example set distribution **MUST** not be evil distribution (a distribution that no hypothesis in $\mathbb{H}$ can get over 50% accuracy, rarely happen)

#### Adaboost

##### Note **weight** can be for anything, the training data, the hypothesis or the parameter in hypothesis.

1. **Initialization**:

-	Initialize the **weights of the training data** for all $i = 1, 2, \dots, m$.
$$
w_i^{(1)} = \frac{1}{m} \quad 
$$
where  $m$  is the number of training examples.

2. **For each iteration  $t$  (from  $t = 1$  to  $T$ )**:
   
-  Train a classifier $h_t(x)$ from the weak learner, minimizes the weighted error.
-  Compute the weighted error of  $h_t$ :

$$\epsilon_t  = \frac{\sum_{i=1}^{m} w_i^{(t)} \mathbf{1}(h_t(x_i) \neq y_i)}{\sum_{i=1}^{m} w_i^{(t)}}$$

where  $\mathbf{1}(\cdot)$  is the indicator function that is 1 if the condition is true and 0 otherwise. 

If $h_t(x_i)$ is a match to $y_i$ can be decide with thresholding (classificaton) or difference smaller than a tolerance value (regression).

- Compute the weight  $\alpha_t$  for the weak classifier based on its error:

$$\alpha_t = \frac{1}{2} \ln \left( \frac{1 - \epsilon_t }{\epsilon_t } \right)$$

This value  $\alpha_t$  indicates the importance or confidence of the weak classifier in the final decision, basically $\alpha_t$ is the **weight of the current hypothesis**.

- update the weight of **data $i$** for $t+1$:

$$w_i^{(t+1)} = w_i^{(t)} e^{-\alpha_t y_i h_t(x_i)}$$

where values of $y_i$ and $h_t(i)$ are either 1 or -1.

or

$$w_i^{(t+1)} = w_i^{(t)} e^{\alpha_t \cdot \mathbb{1}(h_t(x_i) \neq y_i)}$$

where $1(\cdot)$ is indicator function and its value is 1 if the condition is true, otherwise 0.

- after all weight for data are updated, normalize the updated weights:
  
$$Z_t = \sum_{i=1}^{m} w_i^{(t+1)}$$

$$w_i^{(t+1)} = \frac{w_i^{(t+1)}}{Z_t}$$

- then train the next classifier with the new data weight $w_i^{(t+1)}$ for each $x_i$

1. **Final Hypothesis:**

The final classifier is a weighted combination of all the weak classifiers:

$$H(x) = \text{sign} \left( \sum\limits_{t} \alpha_t h_t(x) \right)$$

Where $sign()$ is the sign function, which outputs $1$ if the sum is positive and $-1$ if negative

<br />

- Usually, overfitting is not an issue in Boosting, but for complex artificial neural network (A.N.N) learner tend to make it overfit

---

## Kernel Methods & SVMs (9/10/2024)

### Support Vector Machines (SVM)

For vector $\vec{A}$ ($n \times 1$),  $||A||$ is the norm of $\vec{A}$. Most common form is Euclidean norm ($p = 2$), which is 
$$

\|\mathbf{v}\|_2 = \sqrt{x_1^2 + x_2^2 + \dots + x_n^2}

$$
- represent the straight line distance (magnitude) of the vector

For linearly separable dataset to get:
- hyperplane: $w^TX + b = 0$
- classify each data correctly: $\forall{i}: y_i(w^Tx_i + b) \geqslant 1$, where $y_i \in \{-1, +1\}$
- to get the $w$ and $b$, need to find the maximum margin: $\frac{2}{||w||}$ (minimize overfitting)
- find $w$ and $b$ that maximize margin:
  - $w$: 
    $$
      w: \max(\frac{2}{||w||}) \\ \uparrow\downarrow \\ w: \min(\frac{||w||^2}{2}) \\\uparrow\downarrow\\ \alpha_i: \max(W(\alpha) = \sum\limits_{i}{\alpha_i} - \frac{1}{2}\sum\limits_{ij}{\alpha_i \alpha_j y_iy_jx_i^Tx_j}), \; \alpha_i \geqslant 0, \; \sum\limits_{i}\alpha_i y_i = 0 \\ \downarrow\downarrow \\ w = \sum\limits_{i}{\alpha_i y_i x_i}
    $$
  - $b$: use any $x_i, y_i$ for $b$
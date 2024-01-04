<h1 style="font-size:50px">ECS759P: <i>Artificial Intelligence</i><br>Examination (04/01/2024): SUBMISSION</h1>

## Student details

- **Name**: Pranav Narendra Gopalkrishna
- **Number**: 231052045

## Question 1
### 1.a
Individuals expanded: S-a-d

### 1.b
Individuals expanded: S-a-b-d

### 1.c
#### 1.c (i)

|Node expanded|Agenda|
|---|--- |
|S|a(1, 5, 6)|
|a|b(2, 5, 7), d(6, 2, 8)|
|b|c(3, 4, 7), d(6, 2, 8)|
|c|e(5, 2, 7), d(6, 2, 8)|
|e|G(7, 0, 7), d(6, 2, 8)|
|G|d(6, 2, 8)|

#### 1.c (ii)

- **Path found**: S-a-b-c-e-G
- **Path cost**: 7

### 1.d

Least costs for each node:

- S: 7
- a: 6
- b: 5
- d: 3
- c: 4
- e: 2

The heuristic value for $h_2$ is always less than or equal to the least path costs from any node to the goal. Hence, it is admissible.

### 1.e
$h_1$ is an admissible heuristic, so it never overestimates the true cost from any node to the goal. Hence, it also never overestimates the true cost of any node in the optimal path. Hence, it never skips the optimal path for suboptimal ones, even if the latter are explored first.


## Question 2
### 2.a
#### 2.a (i)
State representation is a string of 6 elements where each element is either T (testify) or R (refuse to testify). The string indices correspond to the rounds. For reference, the string of actions for P1 (player 1): RTRTRT.

#### 2.a (ii)
Chromosome for P2 (player 2): TTTTTT

- Round 1: P1: R, P2: T, P2 payoff = 5
- Round 2: P1: T, P2: T, P2 payoff = 1
- Round 3: P1: R, P2: T, P2 payoff = 5
- Round 4: P1: T, P2: T, P2 payoff = 1
- Round 5: P1: R, P2: T, P2 payoff = 5
- Round 6: P1: T, P2: T, P2 payoff = 1

Total P2 payoff = Fitness value of chromosome TTTTTT = 18

#### 2.b
Chromosome for P2 (player 2): RRTRTR

- Round 1: P1: R, P2: R, P2 payoff = 3
- Round 2: P1: T, P2: R, P2 payoff = 0
- Round 3: P1: R, P2: T, P2 payoff = 5
- Round 4: P1: T, P2: R, P2 payoff = 0
- Round 5: P1: R, P2: T, P2 payoff = 5
- Round 6: P1: T, P2: R, P2 payoff = 0

Total P2 payoff = Fitness value of chromosome RRTRTR = 13

### 2.c

Parents:

- TTTTTT
- RRTRTR

Children:

- c-i = T (from parent 1) + RTR (from parent 2) + TT (from parent 1) = TRTRTT
- c-ii = R (from parent 2) + TTT (from parent 1) + TR (from parent 2) = RTTTTR

For c-i:

- Round 1: P1: R, P2: T, P2 payoff = 5
- Round 2: P1: T, P2: R, P2 payoff = 0
- Round 3: P1: R, P2: T, P2 payoff = 5
- Round 4: P1: T, P2: R, P2 payoff = 0
- Round 5: P1: R, P2: T, P2 payoff = 5
- Round 6: P1: T, P2: T, P2 payoff = 1

Fitness of c-i = 16

For c-ii:

- Round 1: P1: R, P2: R, P2 payoff = 3
- Round 2: P1: T, P2: T, P2 payoff = 1
- Round 3: P1: R, P2: T, P2 payoff = 5
- Round 4: P1: T, P2: T, P2 payoff = 1
- Round 5: P1: R, P2: T, P2 payoff = 5
- Round 6: P1: T, P2: R, P2 payoff = 0

Fitness of c-ii = 15

### 2.d
The genes of the chromosomes at each position do not span the entire search space, even combined, i.e. no amount of recombination of genes using 2-point crossover will generate every possible sequence of actions. Hence, crossover is not enough to explore the entire search space.

To solve this, we use mutation, which is a randomly introduced change to one or more of the genes of a chromosome. A simple mutation method is the use of a single bit mutation, wherein the value of a randomly chosen bit of the chromosome is reversed (T to R or R to T). Over time, such random changes will be able to produce offspring that together can span the search space, thus exploring the entire search space.

### 2.e
#### 2.e (i)

Pool of individuals:

- TTTTTT (parent 1)
- RRTRTR (parent 2)
- TRTRTT (c-i)
- RTTTTR (c-ii)

Total fitness = 18 + 13 + 15 + 16 = 62

Selection probabilities:

- For parent 1: 18/62 = 0.290
- For parent 2: 13/62 = 0.210
- For c-i: 15/62 = 0.242
- For c-ii: 16/62 = 0.258

Cumulative selection probabilities:

- 0.290
- 0.5
- 0.742
- 1.0

#### 2.e (ii)
If the $k$-th random number falls in the range of the $n$-th and $n-1$-th cumulative probabilities, then individual $n$ is chosen as the $k$-th individual.

#### 2.e (iii)
Individuals chosen: parent 2, c-ii

## Question 3
### 3.a
#### 3.a (i)
Smell

#### 3.a (ii)
Test set:

- $x_1 =$ (Shape:A, Colour:Pink, Smell:2, Poisonous:Y)
- $x_2 =$ (Shape:B, Colour:Yellow, Smell:3, Poisonous:N)

For example $x_1$:

- **Level 1**: Smell = 1
- **Level 2**: Colour = Pink
- **Level 3**: Shape = A
- **Leaf**: Yes

$x_1$ is classified as poisonous.

---

For example $x_2$:

- **Level 1**: Smell = 3
- **Leaf**: No

$x_2$ is classified as non-poisonous.

### 3.b
Entropy of a dataset $S$ is given by:

$H(S) = - \sum_{x \in X} P(x) \log_2 P(x)$

Here:

- $X$ is the set of all possible class labels for any $s \in S$
- $P$ is a probability distribution over the set of all possible class labels $X$
- $P(x)$ is the probability of observing class label $x \in X$ for any $s \in S$

Hence, initial entropy of the data set:

$H(S)$

$= - \sum_{x \in {Y, N}} P(x) \log_2 P(x)$

$= - \frac{5}{11} \log_2 \frac{5}{11} - \frac{6}{11} \log_2 \frac{6}{11}$

$= 0.994$

---

Information gain (IG) from splitting by an attribute is given by:

$G(S,Q) = H(S) - \sum_{S_i \in Split(S,Q)} \frac{|S_i|}{|S|} H(S_i)$

Here:

- $S$ is the training dataset
- $Q$ is the attribute by which $S$ is being split into subsets
- $Split(S,Q)$ is the set of all subsets of $S$ formed by spliting $S$ by $Q$
- $|S_i|$ and $|S|$ are the cardinalities of $S_i$ and $S$ respectively
- $H(S_i)$ and $H(S)$ are the entropies of $S_i$ and $S$ respectively

Hence, IG from splitting by smell:

$G(S,Smell) = H(S) - \sum_{S_i \in Split(S,Smell)} \frac{|S_i|}{|S|} H(S_i)$

---

$Split(S, Smell) = {{S|Smell = 1}, {S|Smell = 2}, {S|Smell = 3}}$

---

$H({S|Smell = 1})$

$= - \sum_{x \in {Y, N}} P(x) \log_2 P(x)$ ($P$ defined over ${S|Smell = 1}$)

$= - \frac{3}{3} \log_2 \frac{3}{3} - \frac{0}{3} \log_2 \frac{0}{3}$

$= 0$

---

$H({S|Smell = 2})$

$= - \sum_{x \in {Y, N}} P(x) \log_2 P(x)$ ($P$ defined over ${S|Smell = 2}$)

$= - \frac{2}{5} \log_2 \frac{2}{5} - \frac{3}{5} \log_2 \frac{3}{5}$

$= 0.971$

---

$H({S|Smell = 2})$

$= - \sum_{x \in {Y, N}} P(x) \log_2 P(x)$ ($P$ defined over ${S|Smell = 2}$)

$= - \frac{2}{5} \log_2 \frac{2}{5} - \frac{3}{5} \log_2 \frac{3}{5}$

$= 0.971$

---

$H({S|Smell = 3})$

$= - \sum_{x \in {Y, N}} P(x) \log_2 P(x)$ ($P$ defined over ${S|Smell = 3}$)

$= - \frac{0}{3} \log_2 \frac{3}{3} - \frac{3}{3} \log_2 \frac{0}{3}$

$= 0$

---

Hence, $G(S,Smell) = 0.994 - \frac{3}{11} \times 0 - \frac{5}{11} \times 0.971 - \frac{3}{11} \times 0 = 0.994 - 0.4414 = 0.553$

### 3.c
#### 3.c (i)
Thresholds for splits:

- $BMI < 30$
- BMI $BMI < 36$
- $BMI < 40$

#### 3.c (ii)
Let $P$ denote the probability measure, $H(X)$ denote the entropy of set $X$ and $G(X,Q)$ denote the information gain (IG) from splitting $X$ by attribute or threshold $Q$. The entropy of the training set $S$ is given by:

$H(S)$

$= - \sum_{x \in {\text{yes}, \text{no}}} P(x) \log_2 P(x)$

$= - \frac{3}{7} \log_2 \frac{3}{7} - \frac{4}{7} \log_2 \frac{4}{7}$

$= 0.985$

---

Lowest threshold is BMI $< 30$. Splitting by this threshold, we get subsets:

${S|BMI < 30}, {S|BMI \geq 30}$

Calculating the entropy for each subset...

---

$H({S|BMI < 30})$

$= - \sum_{x \in {\text{yes}, \text{no}}} P(x) \log_2 P(x)$ ($P$ defined over ${S|BMI < 30}$)

$= - \frac{0}{3} \log_2 \frac{3}{3} - \frac{3}{3} \log_2 \frac{0}{3}$

$= 0$

---

$H({S|BMI \geq 30})$

$= - \sum_{x \in {\text{yes}, \text{no}}} P(x) \log_2 P(x)$ ($P$ defined over ${S|BMI \geq 30}$)

$= - \frac{3}{4} \log_2 \frac{3}{4} - \frac{1}{4} \log_2 \frac{1}{4}$

$= 0.811$

---

Hence, information gain from this threshold:

$G(S, BMI < 30)$

$= H(S) - \sum_{S_i \in {{S|BMI < 30}, {S|BMI \geq 30}}} \frac{|S_i|}{|S|} H(S_i)$

$= 0.985 - \frac{3}{7} \times 0 - \frac{4}{7} \times 0.811$

$= 0.807$

### 3.d
#### 3.d (i)
Premise: $\exists x.\forall y.\exists z.P(x, y, z)$

|Step|Result|Remarks|
|--- |--- |--- |
|Remove implications| |Nothing to do|
|Minimise negations| |Nothing to do|
|Skolemise existentials|$\forall y.P(x_0, y, f(y))$|Applied skolem constant $x_0$ & skolem function $f$ under scope of universal $y$|
|Drop universals|$P(x_0, y, f(y))$|Dropped universal quantifier|
|Convert to CNF| | Already in CNF

Result: $P(x_0, y, z_0)$

#### 3.d (ii)
Premise: $\forall x.(\forall y.P(x,y) \rightarrow \exists z.R(x, z))$

|Step|Result|Remarks|
|--- |--- |--- |
|Remove implications|$\forall x.(\lnot (\forall y.P(x,y)) \lor \exists z.R(x, z))$<br>$\equiv \forall x.(\exists y.\lnot P(x,y)) \lor \exists z.R(x, z)$|Applied rule $U \rightarrow V \equiv \lnot U \lor V$|
|Minimise negations| |Nothing to do|
|Skolemise existentials|$\forall x.\lnot P(x,f(x)) \lor R(x, g(x))$|Applied skolem functions $f$ & $g$ under scope of universal $x$|
|Drop universals|$\lnot P(x,f(x)) \lor R(x, g(x))$|Dropped universal quantifier|
|Convert to CNF| | Already in CNF

Result: $\lnot P(x,f(x)) \lor R(x, g(x))$

## Question 4
### 4.a
#### 4.a (i)
Training curve converges slower due to there being more data to fit.


#### 4.a (ii)
Validation curve diverges less from training curve due to more data leading to more generalised model.

### 4.b
#### 4.b (i)
Observed error = Network output - Expected output as given in the training set

#### 4.b (ii)
Partial derivative of output neuron $k$ = Learning rate $\times$ Activation of neuron $k$ $\times$ Delta value for neuron $k$

Delta value for neuron $k$ = Observed error $\times$ Derivative of activation of neuron $k$

#### 4.b (iii)
Partial derivative of hidden-layer neuron $j$ = Learning rate $\times$ Activation of neuron $k$ $\times$ Delta value for neuron $j$

Delta value for neuron $j$ = Derivative of activation of neuron $j$ $\times$ Sum of $w_{j,k} \Delta_k$ for all $k$

Here, $w_{j,k}$ is the weight connecting neuron $j$ to a neuron $k$ in the next layer, while $\Delta_k$ is the delta value for neuron $k$.

### 4.c

For each set of inputs $(x_1, x_2, x_3)$ with observed target $y$:

- Perceptron input = $i = x_1w_1 + x_2w_2 + x_3w_3$
- Perceptron activation = $a = g(i)$
- Observed error = $e = y-a$
- If observed error $\neq 0$, update each weight as $w_i \leftarrow w_i - \alpha x_i e$

**NOTE**: _We have that initially_ $w_1 = w_2 = w_3 = 1$.

Step 1:

- Perceptron input = $i_1 = -1 \times 1 + 2 \times 1 + 1 \times 1$
- Perceptron activation = $g(i_1) = g(2) = 1$
- Observed error = $e_1 = 1-1 = 0$
- No update

Step 2:

- Perceptron input = $i_2 = 3 \times 1 + (-1) \times 1 + 1 \times 1$
- Perceptron activation = $g(i_2) = g(3) = 1$
- Observed error = $e_1 = 0-1 = -1$
- Update weights as follows:
    - $w_1 \leftarrow 1 - 0.25 \times 3 \times (-1) = 1.75$
    - $w_2 \leftarrow 1 - 0.25 \times (-1) \times (-1) = 0.75$
    - $w_3 \leftarrow 1 - 0.25 \times 1 \times (-1) = 1.25$

### 4.d

- Node $k$ input = $i_k = \sum_{j \in {j_1, j_2... j_N}} a_j w_{j,k}$
- Node $k$ activation = $a_k = \sigma(i_k)$

**NOTE 1**: $a_j$ _is either node_ $j$_'s activation or the_ $j$_-th input_.
**NOTE 2**: $\sigma$ _is the sigmoid function._

Node 4:

- Node 4 input = $i_4 = 1 \times w_{1,4} + 1 \times w_{2,4} + 1 \times w_{3,4} = 1.4$
- Node 4 activation = $a_4 = \sigma(i_4) = 0.802$

Node 5:

- Node 5 input = $i_5 = 1 \times w_{1,5} + 1 \times w_{2,5} + 1 \times w_{3,5} = 0$
- Node 5 activation = $a_4 = \sigma(i_4) = 0.5$

Node 7:

- Node 7 input = $i_7 = a_4 \times w_{4,7} + a_5 \times w_{5,7} + 1 \times w_{6,7} = 0.130$
- Node 7 activation = $a_7 = \sigma(i_7) = 0.533$

### 4.e

- For output layer, $\Delta_k = (y'-y)\sigma'(i_k)$, where:
    - $y'$ is the the activation of node $k$
    - $y$ is the observed target value as per the training data
    - $i_k$ is the input to node $k$ before activation
- For hidden layer, $\Delta_j = \sigma'(i_j) w_{j,k} \Delta_k$, where:
    - $\Delta_k$ is the caluclated delta value for the output node
    - $i_j$ is the input to node $j$ before activation

**NOTE 1**: _The above is the case when there is only one output node._
**NOTE 2**: $\sigma$ _is the sigmoid function._

Delta value for node 7 (output node):

$\Delta_7 = (a_7 - 1) \times \sigma'(i_7) = -0.116$

Delta value for node 4 (hidde-layer node):

$\Delta_4 = \sigma'(i_4) \times w_{4,7} \times \Delta_7 = -0.00185$

Updating the weight $w_{1,4}$ (given learning rate $\alpha = 1$):

$w_{1,4} \leftarrow w_{1,4} - 1 \times x_1 \times \Delta_4 = 0.202$

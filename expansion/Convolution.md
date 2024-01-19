# Convolution

## Abstract definition
### Discrete case
Consider an abstract, maybe puzzling problem. Given two lists (i.e. ordered sets) of values $X_1$ and $X_2$, create a new list of values $Y$ such that $Y[k]$ (i.e. the element of $Y$ at index $k$) holds the sum of the products between all $a \in X_1$ and all $b \in X_2$ wherein the index of $a$ in $X_1$ and the index of $b$ in $X_2$ add up to $k$. In other terms, given the following...

- $X_1[i]$ is the element of $X_1$ at index $i$
- $X_2[j]$ is the element of $X_2$ at index $j$
- $|X_1| = n_1$ (size of $X_1$)
- $|X_2| = n_2$ (size of $X_2$)
- $I = \{1, 2 ... n_1\}$
- $J = \{1, 2 ... n_2\}$
- Indices start at $1$

... we have that:

$\displaystyle Y[k] = \sum_{\forall (i \in I, j \in J) | i + j = k} X_1[i] X_2[j] \implies Y[k] = \sum_{i=1}^{n_1} X_1[i] X_2[k - i] = \sum_{i=1}^{n_2} X_1[k - i] X_2[i]$

_This is the convolution operation, notated formally as_ $X_1 * X_2$. More specifically, the $k$-th convolution of $X_1$ and $X_2$ is:

$\displaystyle (X_1 * X_2)_ k = \sum_{i=1}^{n_1} X_1[i] X_2[k - i] = \sum_{i=1}^{n_2} X_1[k - i] X_2[i]$

Note that in the above sums, if $k - i$ goes beyond the indices of $X_2$ or $k - i$ goes beyond the indices of $X_1$, the product is taken as zero. The reason this is justified shall be seen when we see this abstract operation in more specific contexts. Of course, since multiplication is commutative, we could as well rearrange the terms of each product. This means convolution is also commutative, i.e. $(X_1 * X_2)=(X_2 * X_1)$.

### Continuous case
Let $f$ and $g$ be two functions defined on the intervals $A$ and $B$ (either or both could be unbounded). The convolution of $f$ and $g$, notated as $f * g$, is a new function such that:

$\displaystyle (f * g)(n) = \int_{-\infty}^{\infty} \int_{y|x+y=k} f(x)g(y) dy dx = \int_{-\infty}^{\infty} \int_{x|x+y=k} f(x)g(y) dx dy$

$\displaystyle \implies (f * g)(n) = \int_{-\infty}^{\infty} f(x)g(n-x) dx = \int_{-\infty}^{\infty} f(n-x)g(x) dx$

Similar to the discrete case, note that in the above integrals, if $n - x$ goes beyond the domain of either $f$ or $g$, the product is taken as zero. Here too, the reason this is justified shall be seen when we see this abstract operation in more specific contexts. Of course, since multiplication is commutative, we could as well rearrange the terms of each product. This means convolution is also commutative, i.e. $f * g = g * f$.
<br><br>

Note that the definition of convolution in the continuous case generalises the one given in the discrete case. We can see this if we define $f(x) = X_1[x]$ (i.e. the element of $X_1$ at index $x$) and $g(x) = X_2[x]$ (i.e. the element of $X_2$ at index $x$). This is a natural fact when you note that any list (i.e. ordered set) or dictionary (i.e. a mapping between keys and values) is a kind of function, namely a function that maps one discrete value (the index or the key) to another (the value at the index or key); of course, for convolution, we assume that we deal with quantities and not labels. Of course, the integral becomes a summation in the discrete case.

### General case
As we saw, the definition of convolution in the continuous case generalises the one given in the discrete case. To generalise in words, the $n$-th convolution between two functions $f$ and $g$ is the integral (or sum, in the discrete case) of the products between all values of $f$ and all values of $g$ wherein the sum of the preimages (i.e. the inputs to the functions) is $n$. Clearly, convolution between two functions produces an new function (in the discrete case, this function could be in the form of a new list or dictionary) whose domain is the set of all possible sums between elements of the domains of $f$ and $g$.
<br><br>

_What is the point, though?_ We shall see that convolution is a natural way of expressing the sum of two probability distributions. The idea of a convolution, however, extends to moving averages (including weighted moving averages), polynomial multiplication.the filtering of matrices (here, the convolution is defined in multi-dimensional spaces). We shall see how convolution applies to the sum of two probability distributions, but I invite you to consider by yourself its application on moving averages and polynomial multiplication. For reference, I used the video ["But what is a convolution?"](https://www.youtube.com/watch?v=KuXjwB4LzSA), where these other applications are also discussed. We shall, however, explore convolution as it applies in the filtering or processing of matrices, since this is a key aspect of covolutional neural networks.

## Convolution & the sum of two distributions
_Henceforth, "distribution" = "probability distribution" unless stated otherwise._
<br><br>

The assumption underlying everything we shall discuss is that the distributions in question are of independent random processes, i.e. they are independent from each other. In practice, this assumption needs to be verified, of course. Consider the distributions $P_x$ defined for a random process $\theta_x$ whose sample space is $X$, and $P_y$ defined for a random process $\theta_y$ whose sample space is $Y$. Hence, the distribution of $X \times Y$, i.e. the joint outcomes of $\theta_x$ and $\theta_y$ is given by the product measure $P_x \bigotimes P_y$, where:

$P_x \bigotimes P_y(A \subseteq X \times Y) = P_x(A) P_y(A)$

This only expresses the fact that the joint probability of observing two independent events is the probability of observing one event AND the probability of observing the other event (AND implies multiplication, here), no other conditions applied (note that $A$ being a subset of $X \times Y$ means it contains one or more jointly observed events).
<br><br>

The sum operator can be expressed as the function: $+:\mathbb{R}^2 \rightarrow \mathbb{R}, (x, y) \mapsto x + y$. Clearly, $X \times Y \subseteq \mathbb{R}^2$, which means " $+$ " also maps the elements of $X \times Y$ to the elements of $S$ = { $x + y, (x, y) \in X \times Y$ }, i.e. to the set of all possible sums between elements of $X$ and $Y$. Hence, we can define the distribution of $S$ using the distribution of $X \times Y$ and the function " $+$ " as the pushforward measure of $P_x \bigotimes P_y$ through " $+$ ", i.e. $+_* (P_x \bigotimes P_y)$ as $P_x + P_y$. For more clarity, we shall also notate $+_* (P_x \bigotimes P_y)$ as $P_x + P_y$. Then, by the definition of pushforward, for any $U \subseteq S$, we then have that:

$(P_x + P_y)(U) = +_*(P_x \bigotimes P_y)(U) = (P_x \bigotimes P_y)(\{(x, y) \in X \times Y | x + y \in U\})$

In words, the probability mass of any subset $B$ of possible sums between elements of $X$ and $Y$ is exactly the probability mass of every pair from $X \times Y$ whose sum lies in $U$. **_As a side note_**_, know that in the discrete case,_ $U$ _can hold one element alone, but in the continuous case, the probability mass of any discrete set of points (one or many) is zero, so we have to generalise our statements using subsets (which could be continuous too)_.
<br><br>

Fisrt, consider the discrete case, i.e. consider $X$ and $Y$ are discrete sets. Now, consider, what is the probability mass of every pair from $X \times Y$ whose sum lies in $B$? Using the definition of a product measure (since the distribution of these pairs is the product measure $P_x \bigotimes P_y$), and given that $n_x = |X|$ and $n_y = |Y|$, we get the following:

$(P_x + P_y)(t)$

$ = (P_x \bigotimes P_y)(\{(a, b) \in X \times Y | a + b = t\})$

$\displaystyle = \sum_{\{(a, b) \in X \times Y | a + b = t\}} P_x(a) P_y(b)$

$\displaystyle = \sum_a^{n_x} P_x(a) P_y(t - a) = \sum_a^{n_y} P_x(t - a) P_y(a)$

Clearly, if $t - a$ lies outside $Y$, the probability mass will be zero, since it lies outside the support of the distribution $P_y$. The same is the case if $t - a$ lies outside $X$. From the last line, we can clearly see that it is the convolution $P_x * P_y$, i.e. the convolution between the distributions $P_x$ and $P_y$ (which are also kinds of functions). Hence, given that $P_x$ and $P_y$ are independent distributions, we have that:

$P_x + P_y = P_x * P_y$
<br><br>

Of course, we can generalise this in the continuous case, but since the probability mass at a point in the interval is zero yet the probability mass of an interval as such may not be zero, we need to express probability mass as integrals of the probability density function, i.e. PDF. **_As a side note_**_, the PDF is the derivative of the cumulative probability mass, which turns out to be a function such that the area under the curve for some interval_ $[a, b]$ _is in fact the probability mass of this interval under the given distribution. The justification for this is given [here](https://github.com/pranigopu/appliedStatistics/blob/585f2ad9373a779e0a4dfcfcb23304b790522f1a/expansion/QP-Quantifying%20Probability.md)._ Let $f_x$ be the PDF for $P_x$, $f_y$ be the PDF for $P_y$ and $f_{x+y}$ be the PDF of $P_x + P_y$. Then, we have that:

$f_{x+y}(t)$

$\displaystyle = \int_{-\infty}^{\infty} \int_{\{b \in Y | a + b = t\}} P_x(a) P_y(b) db da = \int_{-\infty}^{\infty} \int_{\{a \in X | a + b = t\}} P_x(a) P_y(b) da db$

$\displaystyle = \int_{-\infty}^{\infty}  P_x(a) P_y(t-a) da = \int_{-\infty}^{\infty} P_x(t-a) P_y(a) da$

Again, it is clear that this is the convolution $P_x * P_y$, validating the result for the continuous case as well.

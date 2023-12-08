# ECS759P: _Artificial Intelligence_<br>Assignment 2, Question 1

- **Student name**: Pranav Narendra Gopalkrishna
- **Student number**: 231052045

## Table of contents

- [Key points](#key-points)
- [Statements \& conclusion](#statements--conclusion)
- [Interpretations of certain words \& phrases](#interpretations-of-certain-words--phrases)
- [Initialising knowledge base](#initialising-knowledge-base)
- [Part 1: Converting statements to first-order logic (FOL) expressions](#part-1-converting-statements-to-first-order-logic-fol-expressions)
- [Part 2: Converting FOL expressions to conjunctive normal form (CNF)](#part-2-converting-fol-expressions-to-conjunctive-normal-form-cnf)
	- [Introduction](#introduction)
	- [Purpose](#purpose)
 	- [Method of conversion](#method-of-conversion)
	- [Premise 1](#premise-1)
	- [Premise 2](#premise-2)
	- [Premise 3](#premise-3)
	- [Premise 4](#premise-4)
	- [Premise 5](#premise-5)
	- [Premise 6](#premise-6)
	- [Finalised premises (after converting to CNF)](#finalised-premises-after-converting-to-cnf)
- [Part 3: Formulating, negating \& converting the conclusion](#part-3-formulating-negating--converting-the-conclusion)
- [Part 4: Proof by resolution](#part-4-proof-by-resolution)
	- [Expression pool](#expression-pool)
	- [Unstandardised clauses](#unstandardised-clauses)
	- [Standardised clauses](#standardised-clauses)
	- [Proof by resolution](#proof-by-resolution)

## Key points

- $T$ stands for $True$; if $P$ is a given expression, $P=T$ means $P$ is true
- $F$ stands for $False$; if $P$ is a given expression, $P=F$ means $P$ is false
- "Existential" is shorthand for "variable quantified by existential quantifier"
- "Universal" is shorthand for "variable quantified by universal quantifier"
- If something is true for all, then it is also true for some and for one

## Statements & conclusion

**Statements**:

- You have a dog
- The person you are looking for buys carrots by the bushel
- Anyone who owns a rabbit hates anything that chases any rabbit
- Every dog chases some rabbit
- Anyone who buys carrots by the bushel owns either a rabbit or a grocery store
- Someone who hates something owned by another person will not date that person

_Additional information_...<br>The sentences you just heard reminds you of a person: Robin.

**Conclusion**:

- If the person you are looking for does not own a grocery store, she will not date you

## Interpretations of certain words & phrases

- "Own" means the same as "Have"
- "Anyone who owns a rabbit hates anything that chases any rabbit" means for all $x$, if $x$ is a rabbit & $y$ chases $x$, then the person hates $y$
- "Anyone who buys... " means " All people who buy... "
- "Someone who hates..." means "All people who hate..."
- "The person you are looking for" in this context means "Robin"

Note that we interpret "the person you are looking for" as Robin based on the additional information given after the premises. From the additional information, we interpret that the premises involving "the person you are looking for" hold true for individual named Robin. Furthermore, the final conclusion is a hypothetical involving the person for whom the premises hold true. This interpretation helps make the formulation of logical statements more convenient, since we do not need an extra set of predicates or functions to specify "the person you are looking for."

## Initialising knowledge base

**Predicates**:

- $O(x, y)$: True if $x$ owns $y$
- $H(x, y)$: True if $x$ hates $y$
- $C(x, y)$: True if $x$ chases $y$
- $B(x)$: True if $x$ buys carrots by bushel
- $W(x, y)$: True if $x$ will date $y$
- $D(x)$: True if $x$ is a dog
- $R(x)$: True if $x$ is a rabbit
- $G(x)$: True if $x$ is a grocery store

**Assumption**:

$B(x)$, $O(x, y)$ and $H(x, y)$ can only hold true if $x$ is a person. In other words, when we say that $x$ buys carrots by the bushel, or that $x$ owns / hates / will date $y$, $x$ has to be a person for the predicate to be able to hold true. Furthermore, the predicate $W(x,y)$ presupposes that both $x$ and $y$ are people; if either are not, the predicate cannot hold true.

**Constants**:

- $ROBIN$: Denotes the person named "Robin"
- $YOU$: Denotes the person that is you

## Part 1: Converting statements to first-order logic (FOL) expressions

|Premise ID|Premise expression|
|--- |------ |
|Premise 1|$\exists x \text{ } D(x) \land O(YOU, x)$|
|Premise 2|$B(ROBIN)$|
|Premise 3|$\forall p \text{ } \forall z \text{ } (\exists x \text{ } (R(x) \land O(p, x)) \text{ } \land \exists y \text{ } (R(y) \land C(z, y)) \rightarrow H(p, z))$|
|Premise 4|$\forall x \text{ } (D(x) \rightarrow \exists y \text{ } (R(y) \land C(x, y)))$|
|Premise 5|$\forall p \text{ } (B(p) \rightarrow \exists x \text{ } (O(p, x) \land (R(x) \lor G(x))))$|
|Premise 6|$\forall p \text{ } \forall q \text{ } (\exists x \text{ } (O(p, x) \land H(q, x)) \rightarrow \lnot W(q, p))$| 

**NOTE**: The above premises are logically consistent to each other, i.e. no premise contradicts one or more of the others.

## Part 2: Converting FOL expressions to conjunctive normal form (CNF)

### Introduction

Conjunctive normal form (CNF) is the form of a logical statement wherein the statement consists of one or more disjunctive expressions (expressions consisting of either a single literal or expressions wherein two or more literals are separated by disnjuction, i.e. the OR operation, i.e. $\lor$) connected by conjunction, i.e. the AND operation, i.e. $\land$. For example:

$(A \lor B) \land (C \lor D)$

**NOTE**: Any logical statement has an equivalent CNF statement.

#### Purpose

The methods for resolving (i.e. inferring from) two logical statements are varied and it can be difficult to identify which methods would work best in a given context. By converting the statements to CNF, we are limiting the range of resolution methods applicable, since we are restricting the form of the expression. This makes it easier to automate the process of resolving logical statements, enabling the automation of proving a conclusion from given premises.

#### Method of conversion

For each conversion process, we shall have the following steps:

1. **RI**: Remove implication
2. **MN**: Minimise negations
3. **SE**: Skolemise existentials
4. **DU**:  Drop universals
5. **CNF**: Convert to CNF

**NOTE**: _We shall be using the above abbreviations to indicate these steps later._

---

**_Explaining each step in detail_**...

For explaining the above further, let $U$ and $V$ by two logical expressions, let $K$ and $L$ be two predicates, and let $x$ be a variable.

<u>**1. Removing implications**</u>:

We remove implications using the following rule: $U \rightarrow V \equiv \lnot U \lor V$

<u>**2. Minimising negations**</u>:

Minimising negations is the process of minimising the scope of each negation, i.e. reducing the number of literals to which each negatation '$\lnot$' applies. We minimise negations using the following equivalences:

- Negation to a quantifier:<br>$\lnot \forall x \text{ } ... \equiv \exists x \text{ } \lnot ...$<br>$\lnot \exists x \text{ } ... \equiv \forall x \text{ } \lnot ...$<br>**NOTE**: _The above shall be applied without remarks_
- Double negatives, i.e.:<br>$\lnot \lnot U \equiv U$
- De Morgan's law, i.e.:<br>$\lnot(U \lor V) \equiv \lnot U \land \lnot V$<br>$\lnot(U \land V) \equiv \lnot U \lor \lnot V$

<u>**3. Skolemising existentials**</u>:

Existentials, i.e. existentially quantified variables (ex. $\exists x \text{ } ...$) generally create weak statements, i.e. statements that are less exact in nature, more ambiguous in interpretation and less straightforward to resolve. Skolemisation is the process of removing the usage of existential quantifiers using two methods:

- Skolem constants
- Skolem functions

**_Skolem constants_**...<br>Skolem constants are the simplest form of skolemisation. They apply for existentially quantified variables that are not inside the scope of a universal quantifier, i.e. that do not depend on a universally quantified variable. These existentials may be replaced simply by creating new constants. For example $\exists x \text { } K(x)$ may be changed to $K(c)$, where $c$ is a new constant that does not occur anywhere else in the formula.

**_Skolem functions_**...<br>If an existential $y$ exists in the scope of one or more universal quantifiers, i.e. that depend on one or more universally quantified variables, then we replace $y$ with a unique function that maps the universals in the scope of which $y$ exists to a value that maintains the logical meaning of the statement. The equivalence provides a way for "moving" an existential quantifier before a universal one.

$\forall x \text { } \exists y \text { } L(x,y)\iff \exists f \text { } \forall x \text { } L(x,f(x))$

Here, $f(x)$ is a function that maps $x$ to $y$. Essentially, the sentence...<br>"for every $x$ there exists a $y$ such that $L(x,y)$ holds"<br>... is converted into the logically equivalent statement...<br>"there exists a function $f$ mapping every $x$ into a $y$ such that, for every $x$ it holds that $L(x,f(x))$"

> REFERENCES:
> - https://www.skillvertex.com/blog/what-is-skolemization-in-artificial-intelligence/
> - https://en.wikipedia.org/wiki/Skolem_normal_form

<u>**4. Dropping universals**</u>:

Once existentials are skolemised, universal quantifiers do not add any more meaning to the logical statement than the assumption that all independent variables are universally quantified, because at this point, all independent variables are indeed universally quantified. Hence, we simply drop the universal quantifier in this step.

<u>**5. Convert to CNF**</u>:

After the previous four steps, conversion to CNF would require the application of distributivity alone (if the statement is not already in CNF by this step). Distributivity states that:

- $U_0 \lor (U \land V) \equiv (U_0 \lor U) \land (U_0 \lor V)$
- $U_0 \land (U \lor V) \equiv (U_0 \land U) \lor (U_0 \land V)$

Applying this as needed after dropping universals should be sufficient in obtaining the CNF of the given statement.

### Premise 1

$\exists x \text{ } D(x) \land O(YOU, x)$

|Step|Action|Remarks|
|--- |--- |--- |
|RI|Nothing to do|No implications|
|MN|Nothing to do|No un-minimised negations|
|SE|$D(d) \land O(YOU, d)$|Applied skolem constant $d$|
|DU|Nothing to do|No universals|
|CNF|Nothing to do|Already in CNF|

**Elaborating on remarks**:

 As remarked above, $d$ is the skolem constant used to skolemise the above statement. To elaborate, $d$ is any object such that:<br>$\exists x \text{ } D(x) \land O(YOU, x) \equiv D(d) \land O(YOU, d)$

### Premise 2

$B(ROBIN)$

|Step|Action|Remarks|
|--- |--- |--- |
|RI|Nothing to do|No implications|
|MN|Nothing to do|No un-minimised negations|
|SE|Nothing to do|No existentials|
|DU|Nothing to do|No universals|
|CNF|Nothing to do|Already in CNF|

### Premise 3

$\forall p \text{ } \forall z \text{ } (\exists x \text{ } (R(x) \land O(p, x)) \text{ } \land \exists y \text{ } (R(y) \land C(z, y)) \rightarrow H(p, z))$

|Step|Action|Remarks|
|--- |--- |--- |
|RI|$\forall p \text{ } \forall z \text{ } (\lnot (\exists x \text{ } (R(x) \land O(p, x)) \text{ } \land \exists y \text{ } (R(y) \land C(z, y))) \lor H(p, z))$|Applied $U \rightarrow V \equiv \lnot U \lor V$|
|MN|$\forall p \text{ } \forall z \text{ } (\forall x \text{ } \lnot (R(x) \land O(p, x)) \lor \forall y \text{ } \lnot (R(y) \land C(z, y)) \lor H(p, z))$<br>$\equiv \forall p \text{ } \forall z \text{ } (\forall y \text{ } (\lnot R(x) \lor \lnot O(p, x)) \lor \forall y \text{ } (\lnot R(y) \lor \lnot C(z, y)) \lor H(p, z))$|Applied De Morgan's law twice|
|SE|Nothing to do|No existentials|
|DU|$\lnot R(x) \lor \lnot O(p, x) \lor \lnot R(y) \lor \lnot C(z, y) \lor H(p, z)$|Dropped universal quantifiers|
|CNF|Nothing to do|Already in CNF|

### Premise 4

$\forall x \text{ } (D(x) \rightarrow \exists y \text{ } (R(y) \land C(x, y)))$

|Step|Action|Remarks|
|--- |--- |--- |
|RI|$\forall x \text{ } (\lnot D(x) \lor \exists y \text{ } (R(y) \land C(x, y)))$|Applied $U \rightarrow V \equiv \lnot U \lor V$|
|MN|Nothing to do|No un-minimised negations|
|SE|$\forall x \text{ } (\lnot D(x) \lor (R(f_C(x)) \land C(x, f_C(x))))$|Applied skolem function $f_C$|
|DU|$\lnot D(x) \lor (R(f_C(x)) \land C(x, f_C(x)))$|Dropped universal quantifiers|
|CNF|$(\lnot D(x) \lor R(f_C(x))) \land (\lnot D(x) \lor C(x, f_C(x)))$|Applied distributivity|

**Elaborating on remarks**:

$f_C(x)$ is a function that maps $x$ to a suitable $y$. Practically, we can define $f_C(x)$ or `f_C(x)` as:

```c
f_C(x):
	for all y such that C(x, y)=T do
		if R(y)=T then
			return y // Return a rabbit chased by x
		end if
	end for
	return any y such that C(x, y)=T // Return anything chased by x
```

Note that the above function definition is merely to more concretely interpret the implicit meaning of the skolem function $f_C$, and this function does not need to actually be implemented in practice. In essence, $f_C$ is any function that returns an object for the universal $x$ such that the equivalence of the logical statement is maintained even without the existential $y$ (which is within the scope of $x$).

### Premise 5

$\forall p \text{ } (B(p) \rightarrow \exists x \text{ } ((R(x) \lor G(x)) \land O(p, x)))$

|Step|Action|Remarks|
|--- |--- |--- |
|RI|$\forall p \text{ } (\lnot (B(p)) \lor \exists x \text{ } ((R(x) \lor G(x)) \land O(p, x)))$|Applied $U \rightarrow V \equiv \lnot U \lor V$|
|MN|$\forall p \text{ } ((\lnot B(p)) \lor \exists x \text{ } ((R(x) \lor G(x)) \land O(p, x)))$|Applied De Morgan's law|
|SE|$\forall p \text{ } ((\lnot B(p)) \lor ((R(f_O(p)) \lor G(f_O(p))) \land O(p, f_O(p))))$|Applied skolem function $f_O$|
|DU|$(\lnot B(p)) \lor ((R(f_O(p)) \lor G(f_O(p))) \land O(p, f_O(p)))$|Dropped universal quantifiers|
|CNF|$(\lnot B(p) \lor R(f_O(p)) \lor G(f_O(p))) \land (\lnot B(p) \lor O(p, f_O(p)))$|Applied distributivity|

**Elaborating on remarks**:

$f_O(p)$ is a function that maps $p$ to a suitable $x$. Practically, we can define $f_O(p)$ or `f_O(p)` as:

```c
f_O(x):
	for all y such that O(x, y)=T do
			if R(y)=T or G(y)=T then
				return y // Return a rabbit or grocery store owned by x
			end if
		end for
	return any y such that O(x, y)=T // Return anything owned by x
```

Note that the above function definition is merely to more concretely interpret the implicit meaning of the skolem function $f_O$, and this function does not need to actually be implemented in practice. In essence, $f_O$ is any function that returns an object for the universal $p$ such that the equivalence of the logical statement is maintained even without the existential $x$ (which is within the scope of $p$).

### Premise 6

$\forall p \text{ } \forall q \text{ } (\exists x \text{ } (O(p, x) \land H(q, x)) \rightarrow \lnot W(q, p))$

|Step|Action|Remarks|
|--- |--- |--- |
|RI|$\forall p \text{ } \forall q \text{ } (\lnot(\exists x \text{ } (O(p, x) \land H(q, x))) \lor \lnot W(q, p))$|Applied $U \rightarrow V \equiv \lnot U \lor V$|
|MN|$\forall p \text{ } \forall q \text{ } (\forall x \text{ } \lnot (O(p, x) \land H(q, x))) \lor \lnot W(q, p)$<br>$\equiv \forall p \text{ } \forall q \text{ } (\forall x \text{ } (\lnot O(p, x) \lor \lnot H(q, x)) \lor \lnot W(q, p))$|Applied De Morgan's law twice|
|SE|Nothing to do|No existentials|
|DU|$(\lnot O(p, x) \lor \lnot H(q, x)) \lor \lnot W(q, p)$<br>$\equiv \lnot O(p, x) \lor \lnot H(q, x) \lor \lnot W(q, p)$|1. Dropped universal quantifiers<br>2. Removed extra parantheses|
|CNF|Nothing to do|Already in CNF|

### Finalised premises (after converting to CNF)

|Premise ID|Premise expression|
|--- |--- |
|Premise 1|$D(d) \land O(YOU, d)$|
|Premise 2|$B(ROBIN)$|
|Premise 3|$\lnot R(x) \lor \lnot O(p, x) \lor \lnot R(y) \lor \lnot C(z, y) \lor H(p, z)$|
|Premise 4|$(\lnot D(x) \lor R(f_C(x))) \land (\lnot D(x) \lor C(x, f_C(x)))$|
|Premise 5|$(\lnot B(p) \lor R(f_O(p)) \lor G(f_O(p)))\land (\lnot B(p) \lor O(p, f_O(p)))$|
|Premise 6|$\lnot O(p, x) \lor \lnot H(q, x) \lor \lnot W(q, p)$|

## Part 3: Formulating, negating & converting the conclusion

First-order logic formulation of the conclusion:

$\forall x \text{ } (\lnot(G(x) \land O(ROBIN, x)) \rightarrow \lnot W(ROBIN, YOU))$

Negating the conclusion:

$\lnot(\forall x \text{ } (\lnot(G(x) \land O(ROBIN, x)) \rightarrow \lnot W(ROBIN, YOU)))$

Converting the above to CNF:

|Step|Action|Remarks|
|--- |--- |--- |
|RI|$\lnot(\lnot(\forall x \text{ } \lnot (G(x) \land O(ROBIN, x))) \lor \lnot W(ROBIN, YOU))$|Applied $U \rightarrow V \equiv \lnot U \lor V$|
|MN|$\forall x \text{ } \lnot (G(x) \land O(ROBIN, x)) \land W(ROBIN, YOU)$<br>$\equiv \forall x \text{ } (\lnot G(x) \lor \lnot O(ROBIN, x)) \land W(ROBIN, YOU)$|1. Removed double negatives<br>2. Applied De Morgan's law|
|SE|Nothing to do|No existentials|
|DU|$(\lnot G(x) \lor \lnot O(ROBIN, x)) \land W(ROBIN, YOU)$|Dropped universal quantifiers|
|CNF|Nothing to do|Already in CNF|

## Part 4: Proof by resolution

Proof by resolution is one where, given that the premises are true, we assume the negative of the conclusion is true and look for a contradiction. If we find the contradiction, we know that the negative of the conclusion is false, thus proving the conclusion itself. We will know that a contradiction exists if any two or more of the disjoint clauses from all the CNF statements (including the negated conclusion) resolve to an empty set. Such a resolution means that every term of at least one clause is contradicted at some point, thereby canceling out.

We must first separate the disjuctive clauses from the conjuctive expressions (i.e. we must isolate the sequence of terms connected by OR, i.e. disjunction, from the overall expression of the sequence of disjuctive expressions connected by AND, i.e. conjunction). Following this, we must standardise the variables, so that their reference in each clause is unique and does not conflict with other clauses. This is important because the above clauses do not share any variables, and not giving unique variable identifiers to each clause will cause confusion when applying unifiers or resolving the disjunctive expressions.

### Expression pool

For reference, we must draw clauses from the following:

Source ID|Source expression|
|--- |--- |
|Premise 1|$D(d) \land O(YOU, d)$|
|Premise 2|$B(ROBIN)$|
|Premise 3|$\lnot R(x) \lor \lnot O(p, x) \lor \lnot R(y) \lor \lnot C(z, y) \lor H(p, z)$|
|Premise 4|$(\lnot D(x) \lor R(f_C(x))) \land (\lnot D(x) \lor C(x, f_C(x)))$|
|Premise 5|$(\lnot B(p) \lor R(f_O(p)) \lor G(f_O(p)))\land (\lnot P(p) \lor \lnot B(p) \lor O(p, f_O(p)))$|
|Premise 6|$\lnot O(p, x) \lor \lnot H(q, x) \lor \lnot W(q, p)$|
|Negated conclusion|$(\lnot G(x) \lor \lnot O(ROBIN, x)) \land (W(ROBIN, YOU))$|

### Unstandardised clauses

|ID|Clause|Source ID|
|--- |--- |--- |
|01|$D(d)$|Premise 1|
|02|$O(YOU, d)$|Premise 1|
|03|$B(ROBIN)$|Premise 2|
|04|$\lnot R(x) \lor \lnot O(p, x) \lor \lnot R(y) \lor \lnot C(z, y) \lor H(p, z)$|Premise 3|
|05|$\lnot D(x) \lor R(f_C(x))$|Premise 4|
|06|$\lnot D(x) \lor C(x, f_C(x))$|Premise 4|
|07|$\lnot B(p) \lor R(f_O(p)) \lor G(f_O(p))$|Premise 5|
|08|$\lnot B(p) \lor O(p, f_O(p))$|Premise 5|
|09|$\lnot O(p, x) \lor \lnot H(q, x) \lor \lnot W(q, p)$|Premise 6|
|10|$\lnot G(x) \lor \lnot O(ROBIN, x)$|Negated conclusion|
|11|$W(ROBIN, YOU)$|Negated conclusion|

### Standardised clauses

|ID|Clause|Source ID|
|--- |--- |--- |
|01|$D(d)$|Premise 1|
|02|$O(YOU, d)$|Premise 1|
|03|$B(ROBIN)$|Premise 2|
|04|$\lnot R(x_1) \lor \lnot O(x_2, x_1) \lor \lnot R(x_3) \lor \lnot C(x_4, x_3) \lor H(x_2, x_4)$|Premise 3|
|05|$\lnot D(x_5) \lor R(f_C(x_5))$|Premise 4|
|06|$\lnot D(x_6) \lor C(x_6, f_C(x_6))$|Premise 4|
|07|$\lnot B(x_7) \lor R(f_O(x_7)) \lor G(f_O(x_7))$|Premise 5|
|08|$\lnot B(x_8) \lor O(x_8, f_O(x_8))$|Premise 5|
|09|$\lnot O(x_9, x_{10}) \lor \lnot H(x_{11}, x_{10}) \lor \lnot W(x_{11}, x_9)$|Premise 6|
|10|$\lnot G(x_{12}) \lor \lnot O(ROBIN, x_{12})$|Negated conclusion|
|11|$W(ROBIN, YOU)$|Negated conclusion|

### Proof by resolution

Proof by resolution is done using three operations:

1. Unification
2. Factoring
3. Resolution

<u>**1. Unification**</u>:

Unification is the process of instantiating variables of one or more clauses with relevant constants or functions. In general, unification is represented using a unifier of the form: { $x_{new}/x_{old}, y_{new}/y_{old}...$ }. Here, $x_1/x_2$ means $x_1$ replaces $x_2$. We can replace multiple variables in this manner, separating each pair of variables and their replacements using commas.

<u>**2. Factoring**</u>:

Factoring is the process of removing all duplicates of a literal in a disjunctive clause (i.e. a clause wherein each literal is separated by a disjunction, i.e. OR, i.e. $\lor$). This is because $U \lor U \lor ... \lor U \equiv U$.

<u>**3. Resolution**</u>:

Given that clauses $C_1$ and $C_2$ are two disjuctive clauses such that they contain at least one pair of complementary literals (i.e. $C_1$ contains at least one literal $A$ such that $\lor A$ is present in $C_2$), resolution is the process of reducing the conjunction of $C_1$ and $C_2$, i.e. $C_1 \land C_2$ to a single disjunctive clause containing all the literals of $C_1$ and $C_2$ except the complementary literals. In other terms, if $A$, $B$ and $C$ are three literals, then:

$(A \lor B) \land (\lnot A \lor C) \equiv B \lor C$

---

For the following proof, we have mainly used unification and resolution. Note that always resolution follows unification, i.e. we resolve clauses after applying the unifier. The given unifier applies to both of the clauses mentioned in the "Clauses" column, and the resolved clause in the "Result" column is the new disjunctive clause after resolution. The resolved clause can later be referrenced using the number given in the "ID" column for the row where the resolution took place; hence, the "ID" applies to the resolved clause. The resolution as well as the clauses involved have been labelled with their ID anyway (in the form `<id>: <expression>`) for extra clarity.

---

|ID|Clauses|Unifier|Result|
|--- |--- |--- |--- |
|14|{07, 10}|{ $f_O(x_7)/x_{12}$, $ROBIN/x_7$ }|Unified clauses:<br>07: $\lnot B(ROBIN) \lor R(f_O(ROBIN)) \lor G(f_O(ROBIN))$<br>10: $\lnot G(f_O(ROBIN)) \lor \lnot O(ROBIN, f_O(ROBIN))$<br><br>Resolution:<br>14: $\lnot B(ROBIN) \lor R(f_O(ROBIN)) \lor \lnot O(ROBIN, f_O(ROBIN))$|
|15|{04, 05}|{ $x_4/x_5$, $f_C(x_4)/x_3$ }|Unified clauses:<br>04: $\lnot R(x_1) \lor \lnot O(x_2, x_1) \lor \lnot R(f_C(x_4)) \lor \lnot C(x_4, f_C(x_4)) \lor H(x_2, x_4)$<br>05: $\lnot D(x_4) \lor R(f_C(x_4))$<br><br>Resolution:<br>15: $\lnot R(x_1) \lor \lnot O(x_2, x_1) \lor \lnot C(x_4, f_C(x_4)) \lor H(x_2, x_4) \lor \lnot D(x_4)$|
|16|{06, 15}|{ $x_4/x_6$ }|Unified clauses:<br>06: $\lnot D(x_4) \lor C(x_4, f_C(x_4))$<br>15: $\lnot R(x_1) \lor \lnot O(x_2, x_1) \lor \lnot C(x_4, f_C(x_4)) \lor H(x_2, x_4) \lor \lnot D(x_4)$<br><br>Resolution:<br>16: $\lnot R(x_1) \lor \lnot O(x_2, x_1) \lor H(x_2, x_4) \lor \lnot D(x_4)$|
|17|{09, 16}|{ $x_2/x_{11}$, $x_4/x_{10}$ }|Unified clauses:<br>09: $\lnot O(x_9, x_{10}) \lor \lnot H(x_2, x_4) \lor \lnot W(x_4, x_9)$<br>16: $\lnot R(x_1) \lor \lnot O(x_2, x_1) \lor H(x_2, x_4) \lor \lnot D(x_4)$<br><br>Resolution:<br>17: $\lnot R(x_1) \lor \lnot O(x_2, x_1) \lor \lnot D(x_4) \lor \lnot O(x_9, x_4) \lor \lnot W(x_2, x_9)$|
|18|{14, 17}|{ $f_O(x_2)/x_1$, $ROBIN/x_2$ }|Unified clauses:<br>14: $\lnot B(ROBIN) \lor R(f_O(ROBIN)) \lor \lnot O(ROBIN, f_O(ROBIN))$<br>17: $\lnot R(f_O(ROBIN)) \lor \lnot O(ROBIN, f_O(ROBIN)) \lor \lnot D(x_4) \lor \lnot O(x_9, x_4) \lor \lnot W(ROBIN, x_9)$<br><br>Resolution:<br>18: $\lnot O(ROBIN, f_O(ROBIN)) \lor \lnot D(x_4) \lor \lnot O(x_9, x_4) \lor \lnot W(ROBIN, x_9) \lor \lnot B(ROBIN)$|
|19|{08, 18}|{ $ROBIN/x_8$ }|Unified clauses:<br>08: $\lnot B(ROBIN) \lor O(ROBIN, f_O(ROBIN))$<br>18: $\lnot O(ROBIN, f_O(ROBIN)) \lor \lnot D(x_4) \lor \lnot O(x_9, x_4) \lor \lnot W(ROBIN, x_9) \lor \lnot B(ROBIN)$<br><br>Resolution:<br>19: $\lnot D(x_4) \lor \lnot O(x_9, x_4) \lor \lnot W(ROBIN, x_9) \lor \lnot B(ROBIN)$|
|20|{01, 19}|{ $d/x_4$ }|Unified clauses:<br>01: $D(d)$<br>19: $\lnot D(x_4) \lor \lnot O(x_9, x_4) \lor \lnot W(ROBIN, x_9) \lor \lnot B(ROBIN)$<br><br>Resolution:<br>20: $\lnot O(x_9, d) \lor \lnot W(ROBIN, x_9) \lor \lnot B(ROBIN)$|
|21|{02, 20}|{ $YOU/x_9$ }|Unified clauses:<br>02: $O(YOU, d)$<br>20: $\lnot O(YOU, d) \lor \lnot W(ROBIN, YOU) \lor \lnot B(ROBIN)$<br><br>Resolution:<br>21: $\lnot W(ROBIN, YOU) \lor \lnot B(ROBIN)$|
|22|{11, 21}|None|Unified clauses:<br>11: $W(ROBIN, YOU)$<br>21: $\lnot W(ROBIN, YOU) \lor \lnot B(ROBIN)$<br><br>Resolution:<br>22: $\lnot B(ROBIN)$|
|23|{03, 22}|None|Unified clauses:<br>11: $B(ROBIN)$<br>21: $\lnot B(ROBIN)$<br><br>Resolution:<br>22: { $\text { }$ }|

**NOTE**: Factoring was used for resolution 19, where repetitions of $\lnot B(ROBIN)$ were removed.

---

We see that with the above sequence of steps and with the right unifiers, we were able to negate the selected clauses completely under the assumption that the negated conclusion was true, i.e. we obtained a contradiction by assuming the negated conclusion. Since the premises were logically consistent, the contradiction could only have arisen from the inclusion of the negated conclusion. This implies that, since the negated conclusion is clearly false given the contradiction, the conclusion is true. More specifically, the following hypothetical is true:

_"If the person you are looking for, i.e. Robin, does not own a grocery store, she will not date you."_

Hence, you have a shot at getting a date with Robin if she does own a grocery store; whether or not she does own one is not given.

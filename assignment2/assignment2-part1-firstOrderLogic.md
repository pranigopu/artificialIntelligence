# ECS759P: _Artificial Intelligence_<br>Assignment 2, Question 1

## Key points

- $T$ stands for $True$; if $P$ is a given expression, $P=T$ means $P$ is true
- $F$ stands for $False$; if $P$ is a given expression, $P=F$ means $P$ is false
- "Existential" is shorthand for "variable quantified by existential quantifier"
- "Universal" is shorthand for "variable quantified by universal quantifier"

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

## Definitions

**Predicates**:

- $O(x, y)$: True if $x$ owns $y$
- $H(x, y)$: True if $x$ hates $y$
- $C(x, y)$: True if $x$ chases $y$
- $B(x)$: True if $x$ buys carrots by bushel
- $W(x, y)$: True if $x$ will date $y$
- $D(x)$: True if $x$ is a dog
- $R(x)$: True if $x$ is a rabbit
- $P(x)$: True if $x$ is a person
- $G(x)$: True if $x$ is a grocery store

**Constants**:

- $ROBIN$: Indicates the individual named "Robin"
- $YOU$: Indicates the individual that is you

## Part 1

<table>
	<thead>
		<th>Premise ID</th>
		<th width=600px>Premise expression</th>
	</thead>
	<tbody>
        <tr>
            <td>Premise 1</td>
            <td>$\exists x \text{ } D(x) \land O(YOU, x)$</td>
        </tr>
        <tr>
            <td>Premise 2</td>
            <td>$B(ROBIN)$</td>
        </tr>
        <tr>
            <td>Premise 3</td>
            <td>$\forall p \text{ } \forall z \text{ } (P(p) \land \exists x \text{ } (R(x) \land O(p, x)) \text{ } \land \exists y \text{ } (R(y) \land C(z, y)) \rightarrow H(p, z))$</td>
        </tr>
        <tr>
            <td>Premise 4</td>
            <td>$\forall x \text{ } (D(x) \rightarrow \exists y \text{ } (R(y) \land C(x, y)))$</td>
        </tr>
        <tr>
            <td>Premise 5</td>
            <td>$\forall p \text{ } (P(p) \land B(p) \rightarrow \exists x \text{ } (O(p, x) \land (R(x) \lor G(x))))$</td>
        </tr>
        <tr>
            <td>Premise 6</td>
            <td>$\forall p \text{ } \forall q \text{ } (P(p) \land P(q) \land \exists x \text{ } (O(q, x) \land H(p, x)) \rightarrow \lnot W(p, q))$</td>
        </tr>
	</tbody>
</table>

**NOTE**: If something is true for all, then it is also true for some and for one.

## Part 2

Transforming the statements to conjunctive normal form (CNF), i.e. a conjunct of disjuncts (product of sums, i.e. "AND of OR's").

**NOTE 1**: We can remove the universal quantifier safely when there are no variables with existential quantifiers to which the universally quantified variable maps to.

**NOTE 2**: When replacing the existential quantifier with a function $f$ of a universally quantified variable $x$, we use the same function $f$ throughout the premises, because the existential quantifier means at least one object is such that the condition involving $x$ holds true. $f$ is defined so that it maps each possible value of $x$ to a particular object accordingly.

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

For explaining the above further, let $U$ and $V$ by two logical expressions, let $S$ and $T$ be two predicates, and let $x$ be a variable.

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

**_Skolem constants_**...<br>Skolem constants are the simplest form of skolemisation. They apply for existentially quantified variables that are not inside the scope of a universal quantifier, i.e. that do not depend on a universally quantified variable. These existentials may be replaced simply by creating new constants. For example $\exists x \text { } S(x)$ may be changed to $S(c)$, where $c$ is a new constant that does not occur anywhere else in the formula.

**_Skolem functions_**...<br>If an existential $y$ exists in the scope of one or more universal quantifiers, i.e. that depend on one or more universally quantified variables, then we replace $y$ with a unique function that maps the universals in the scope of which $y$ exists to a value that maintains the logical meaning of the statement. The equivalence provides a way for "moving" an existential quantifier before a universal one.

$\forall x \text { } \exists y \text { } T(x,y)\iff \exists f \text { } \forall x \text { } T(x,f(x))$

Here, $f(x)$ is a function that maps $x$ to $y$. Essentially, the sentence...<br>"for every $x$ there exists a $y$ such that $T(x,y)T"<br>... is converted into the logically equivalent statement...<br>"there exists a function $f$ mapping every $x$ into a $y$ such that, for every $x$ it holds that $T(x,f(x))$"

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

<table>
	<thead>
		<tr>
			<th width=50px>Step</th>
			<th width=500px>Action(s)</th>
			<th>Remarks</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>RI</td>
			<td>Nothing to do</td>
			<td>No implications</td>
		</tr>
		<tr>
			<td>MN</td>
			<td>Nothing to do</td>
			<td>No un-minimised negations</td>
		</tr>
		<tr>
			<td>SE</td>
			<td>$D(d) \land O(YOU, d)$</td>
			<td>Applied skolem constant $d$</td>
		</tr>
		<tr>
			<td>DU</td>
			<td>Nothing to do</td>
			<td>No universals</td>
		</tr>
		<tr>
			<td>CNF</td>
			<td>Nothing to do</td>
			<td>Already in CNF</td>
		</tr>
	</tbody>
</table>

**Elaborating on remarks**:

 As remarked above, $d$ is the skolem constant used to skolemise the above statement. To elaborate, $d$ is any object such that:<br>$\exists x \text{ } D(x) \land O(YOU, x) \equiv D(d) \land O(YOU, d)$

### Premise 2

$B(ROBIN)$

<table>
	<thead>
		<tr>
			<th width=50px>Step</th>
			<th width=500px>Action(s)</th>
			<th>Remarks</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>RI</td>
			<td>Nothing to do</td>
			<td>No implications</td>
		</tr>
		<tr>
			<td>MN</td>
			<td>Nothing to do</td>
			<td>No un-minimised negations</td>
		</tr>
		<tr>
			<td>SE</td>
			<td>Nothing to do</td>
			<td>No existentials</td>
		</tr>
		<tr>
			<td>DU</td>
			<td>Nothing to do</td>
			<td>No universals</td>
		</tr>
		<tr>
			<td>CNF</td>
			<td>Nothing to do</td>
			<td>Already in CNF</td>
		</tr>
	</tbody>
</table>

### Premise 3

$\forall p \text{ } \forall z \text{ } (P(p) \land \exists x \text{ } (R(x) \land O(p, x)) \text{ } \land \exists y \text{ } (R(y) \land C(z, y)) \rightarrow H(p, z))$

<table>
	<thead>
		<tr>
			<th width=50px>Step</th>
			<th width=500px>Action(s)</th>
			<th>Remarks</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>RI</td>
			<td>
				$\forall p \text{ } \forall z \text{ } (\lnot (P(p) \land \exists x \text{ } (R(y) \land O(p, y)) \text{ } \land \exists y \text{ } (R(y) \land C(z, y))) \lor H(p, z))$
			</td>
			<td>Applied $U \rightarrow V \equiv \lnot U \lor V$</td>
		</tr>
		<tr>
			<td>MN</td>
			<td>
				$\forall p \text{ } \forall z \text{ } (\lnot P(p) \lor \lnot \exists x \text{ } (R(x) \land O(p, x)) \lor \lnot \exists y \text{ } (R(y) \land C(z, y)) \lor H(p, z))$
				<br>
				$\equiv \forall p \text{ } \forall z \text{ } (\lnot P(p) \lor \forall x \text{ } \lnot (R(x) \land O(p, x)) \lor \forall y \text{ } \lnot (R(y) \land C(z, y)) \lor H(p, z))$
				<br>
				$\equiv \forall p \text{ } \forall z \text{ } (\lnot P(p) \lor \forall y \text{ } (\lnot R(x) \lor \lnot O(p, x)) \lor \forall y \text{ } (\lnot R(y) \lor \lnot C(z, y)) \lor H(p, z))$
			</td>
			<td>Applied De Morgan's law thrice</td>
		</tr>
		<tr>
			<td>SE</td>
			<td>Nothing to do</td>
			<td>No existentials</td>
		</tr>
		<tr>
			<td>DU</td>
			<td>
				$\lnot P(p) \lor \lnot R(x) \lor \lnot O(p, x) \lor \lnot R(y) \lor \lnot C(z, y) \lor H(p, z)$
			</td>
			<td>Dropped universal quantifiers</td>
		</tr>
		<tr>
			<td>CNF</td>
			<td>Nothing to do</td>
			<td>Already in CNF</td>
		</tr>
	</tbody>
</table>

### Premise 4

$\forall x \text{ } (D(x) \rightarrow \exists y \text{ } (R(y) \land C(x, y)))$

<table>
	<thead>
		<tr>
			<th width=50px>Step</th>
			<th width=500px>Action(s)</th>
			<th>Remarks</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>RI</td>
			<td>
				$\forall x \text{ } (\lnot D(x) \lor \exists y \text{ } (R(y) \land C(x, y)))$
			</td>
			<td>Applied $U \rightarrow V \equiv \lnot U \lor V$</td>
		</tr>
		<tr>
			<td>MN</td>
			<td>Nothing to do</td>
			<td>No un-minimised negations</td>
		</tr>
		<tr>
			<td>SE</td>
			<td>
				$\forall x \text{ } (\lnot D(x) \lor (R(f_C(x)) \land C(x, f_C(x))))$
			</td>
			<td>Applied skolem function $f_C$</td>
		</tr>
		<tr>
			<td>DU</td>
			<td>
				$\lnot D(x) \lor (R(f_C(x)) \land C(x, f_C(x)))$
			</td>
			<td>Dropped universal quantifiers</td>
		</tr>
		<tr>
			<td>CNF</td>
			<td>
				$(\lnot D(x) \lor R(f_C(x))) \land (\lnot D(x) \lor C(x, f_C(x)))$
			</td>
			<td>Applied distributivity</td>
		</tr>
	</tbody>
</table>

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

Note that the above function definition is merely to clarify the implicit meaning of the skolem function $f_C$, and this function does not need to actually be implemented in practice. In essence, $f_C$ is any function that returns an object for the universal $x$ such that the equivalence of the logical statement is maintained even without the existential $y$ (which is within the scope of $x$).

### Premise 5

$\forall p \text{ } (P(p) \land B(p) \rightarrow \exists x \text{ } ((R(x) \lor G(x)) \land O(p, x)))$

<table>
	<thead>
		<tr>
			<th width=50px>Step</th>
			<th width=500px>Action(s)</th>
			<th>Remarks</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>RI</td>
			<td>
				$\forall p \text{ } (\lnot (P(p) \land B(p)) \lor \exists x \text{ } ((R(x) \lor G(x)) \land O(p, x)))$
			</td>
			<td>Applied $U \rightarrow V \equiv \lnot U \lor V$</td>
		</tr>
		<tr>
			<td>MN</td>
			<td>
				$\forall p \text{ } ((\lnot P(p) \lor \lnot B(p)) \lor \exists x \text{ } ((R(x) \lor G(x)) \land O(p, x)))$
			</td>
			<td>Applied De Morgan's law</td>
		</tr>
		<tr>
			<td>SE</td>
			<td>
				$\forall p \text{ } ((\lnot P(p) \lor \lnot B(p)) \lor ((R(f_O(p)) \lor G(f_O(p))) \land O(p, f_O(p))))$
			</td>
			<td>Applied skolem function $f_O$</td>
		</tr>
		<tr>
			<td>DU</td>
			<td>
				$(\lnot P(p) \lor \lnot B(p)) \lor ((R(f_O(p)) \lor G(f_O(p))) \land O(p, f_O(p)))$
			</td>
			<td>Dropped universal quantifiers</td>
		</tr>
		<td>CNF</td>
			<td>
				$(\lnot P(p) \lor \lnot B(p) \lor R(f_O(p)) \lor G(f_O(p))) \land (\lnot P(p) \lor \lnot B(p) \lor O(p, f_O(p)))$
			</td>
			<td>Applied distributivity</td>
		</tr>
	</tbody>
</table>

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

Note that the above function definition is merely to clarify the implicit meaning of the skolem function $f_O$, and this function does not need to actually be implemented in practice. In essence, $f_O$ is any function that returns an object for the universal $p$ such that the equivalence of the logical statement is maintained even without the existential $x$ (which is within the scope of $p$).

### Premise 6

$\forall p \text{ } \forall q \text{ } (P(p) \land P(q) \land \exists x \text{ } (O(q, x) \land H(p, x)) \rightarrow \lnot W(p, q))$

<table>
	<thead>
		<tr>
			<th width=50px>Step</th>
			<th width=500px>Action(s)</th>
			<th>Remarks</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>RI</td>
			<td>
				$\forall p \text{ } \forall q \text{ } (\lnot(P(p) \land P(q) \land \exists x \text{ } (O(q, x) \land H(p, x))) \lor \lnot W(p, q))$
			</td>
			<td>Applied $U \rightarrow V \equiv \lnot U \lor V$</td>
		</tr>
		<tr>
			<td>MN</td>
			<td>
				$\forall p \text{ } \forall q \text{ } (\lnot P(p) \lor \lnot P(q) \lor \lnot (\exists x \text{ } (O(q, x) \land H(p, x))) \lor \lnot W(p, q))$
				<br>
				$\equiv \forall p \text{ } \forall q \text{ } (\lnot P(p) \lor \lnot P(q) \lor \forall x \text{ } \lnot (O(q, x) \land H(p, x))) \lor \lnot W(p, q))$
				<br>
				$\equiv \forall p \text{ } \forall q \text{ } (\lnot P(p) \lor \lnot P(q) \lor \forall x \text{ } (\lnot O(q, x) \lor \lnot H(p, x)) \lor \lnot W(p, q))$
			</td>
			<td>Applied De Morgan's law thrice</td>
		</tr>
		<tr>
			<td>SE</td>
			<td>Nothing to do</td>
			<td>No existentials</td>
		</tr>
		<tr>
			<td>DU</td>
			<td>
				$\lnot P(p) \lor \lnot P(q) \lor (\lnot O(q, x) \lor \lnot H(p, x)) \lor \lnot W(p, q)$
				<br>
				$\equiv \lnot P(p) \lor \lnot P(q) \lor \lnot O(q, x) \lor \lnot H(p, x) \lor \lnot W(p, q)$
			</td>
			<td>1. Dropped universal quantifiers<br>2. Removed extra parantheses</td>
		</tr>
		<tr>
			<td>CNF</td>
			<td>Nothing to do</td>
			<td>Already in CNF</td>
		</tr>
	</tbody>
</table>

### Finalised premises (before standardising variables)

<table>
	<thead>
		<th>Premise ID</th>
		<th width=600px>Premise expression</th>
	</thead>
	<tbody>
        <tr>
            <td>Premise 1</td>
            <td>$D(d) \land O(YOU, d)$</td>
        </tr>
        <tr>
            <td>Premise 2</td>
            <td>$B(ROBIN)$</td>
        </tr>
        <tr>
            <td>Premise 3</td>
            <td>$\lnot P(p) \lor \lnot R(x) \lor \lnot O(p, x) \lor \lnot R(y) \lor \lnot C(z, y) \lor H(p, z)$</td>
        </tr>
        <tr>
            <td>Premise 4</td>
            <td>$(\lnot D(x) \lor R(f_C(x))) \land (\lnot D(x) \lor C(x, f_C(x)))$</td>
        </tr>
        <tr>
            <td>Premise 5</td>
            <td>$(\lnot P(p) \lor \lnot B(p) \lor R(f_O(p)) \lor G(f_O(p)))\land (\lnot P(p) \lor \lnot B(p) \lor O(p, f_O(p)))$</td>
        </tr>
        <tr>
            <td>Premise 6</td>
            <td>$\lnot P(p) \lor \lnot P(q) \lor \lnot O(q, x) \lor \lnot H(p, x) \lor \lnot W(p, q)$</td>
        </tr>
	</tbody>
</table>

## Part 3

First-order logic formulation of the conclusion:

$\forall x \text{ } (\lnot(G(x) \land O(ROBIN, x)) \rightarrow \lnot W(ROBIN, YOU))$

Negating the conclusion:

$\lnot(\forall x \text{ } (\lnot(G(x) \land O(ROBIN, x)) \rightarrow \lnot W(ROBIN, YOU)))$

Converting the above to CNF:

<table>
	<thead>
		<tr><th width=50px></th><th width=500px></th></tr>
	</thead>
	<tbody>
		<tr>
			<td>RI</td>
			<td>
				$\lnot(\lnot(\forall x \text{ } \lnot (G(x) \land O(ROBIN, x))) \lor \lnot W(ROBIN, YOU))$
			</td>
			<td>Applied $U \rightarrow V \equiv \lnot U \lor V$</td>
		</tr>
		<tr>
			<td>MN</td>
			<td>
				$\forall x \text{ } \lnot (G(x) \land O(ROBIN, x)) \land W(ROBIN, YOU)$
				<br>
				$\equiv \forall x \text{ } (\lnot G(x) \lor \lnot O(ROBIN, x)) \land W(ROBIN, YOU)$
			</td>
			<td>1. Removed double negatives<br>2. Applied De Morgan's law</td>
		</tr>
		<tr>
			<td>SE</td>
			<td>Nothing to do</td>
			<td>No existentials</td>
		</tr>
		<tr>
			<td>DU</td>
			<td>
				$(\lnot G(x) \lor \lnot O(ROBIN, x)) \land W(ROBIN, YOU)$
			</td>
			<td>Dropped universal quantifiers</td>
		</tr>
		<tr>
			<td>CNF</td>
			<td>Nothing to do</td>
			<td>Already in CNF</td>
		</tr>
	</tbody>
</table>

## Part 4

Proof by resolution is one where, given that the premises are true, we assume the negative of the conclusion is true and look for a contradiction. If we find the contradiction, we know that the negative of the conclusion is false, thus proving the conclusion itself. We will know that a contradiction exists if any two or more of the disjoint clauses from all the CNF statements (including the negated conclusion) resolve to an empty set. Such a resolution means that every term of at least one clause is contradicted at some point, thereby canceling out.

We must first separate the disjuctive clauses from the conjuctive expressions (i.e. we must isolate the sequence of terms connected by OR, i.e. disjunction, from the overall expression of the sequence of disjuctive expressions connected by AND, i.e. conjunction). Following this, we must standardise the variables, so that their reference in each clause is unique and does not conflict with other clauses. This is important because the above clauses do not share any variables, and not giving unique variable identifiers to each clause will cause confusion when applying unifiers or resolving the disjunctive expressions.

### Expression pool

For reference, we must draw clauses from the following:

<table>
	<thead>
		<th>Source ID</th>
		<th width=600px>Source expression</th>
	</thead>
	<tbody>
        <tr>
            <td>Premise 1</td>
            <td>$D(d) \land O(YOU, d)$</td>
        </tr>
        <tr>
            <td>Premise 2</td>
            <td>$B(ROBIN)$</td>
        </tr>
        <tr>
            <td>Premise 3</td>
            <td>$\lnot P(p) \lor \lnot R(x) \lor \lnot O(p, x) \lor \lnot R(y) \lor \lnot C(z, y) \lor H(p, z)$</td>
        </tr>
        <tr>
            <td>Premise 4</td>
            <td>$(\lnot D(x) \lor R(f_C(x))) \land (\lnot D(x) \lor C(x, f_C(x)))$</td>
        </tr>
        <tr>
            <td>Premise 5</td>
            <td>$(\lnot P(p) \lor \lnot B(p) \lor R(f_O(p)) \lor G(f_O(p)))\land (\lnot P(p) \lor \lnot B(p) \lor O(p, f_O(p)))$</td>
        </tr>
        <tr>
            <td>Premise 6</td>
            <td>$\lnot P(p) \lor \lnot P(q) \lor \lnot O(q, x) \lor \lnot H(p, x) \lor \lnot W(p, q)$</td>
        </tr>
        <tr>
            <td>Negated conclusion</td>
            <td>$(\lnot G(a) \lor \lnot O(ROBIN, a)) \land (W(ROBIN, YOU))$</td>
        </tr>
        <tr>
            <td>Given 1</td>
            <td>$P(ROBIN)$</td>
        </tr>
        <tr>
            <td>Given 2</td>
            <td>$P(YOU)$</td>
        </tr>
	</tbody>
</table>

### Unstandardised clauses:

<table>
	<thead>
		<th>ID</th>
		<th width=600px>Clause</th>
		<th>Source ID</th>
	</thead>
	<tbody>
        <tr>
            <td>1</td>
            <td>$D(d)$</td>
            <td>Premise 1</td>
        </tr>
				<tr>
            <td>2</td>
            <td>$O(YOU, d)$</td>
            <td>Premise 1</td>
        </tr>
        <tr>
            <td>3</td>
            <td>$B(ROBIN)$</td>
            <td>Premise 2</td>
        </tr>
        <tr>
            <td>4</td>
            <td>$\lnot P(p) \lor \lnot R(x) \lor \lnot O(p, x) \lor \lnot R(y) \lor \lnot C(z, y) \lor H(p, z)$</td>
            <td>Premise 3</td>
        </tr>
        <tr>
            <td>5</td>
            <td>$\lnot D(x) \lor R(f_C(x))$</td>
            <td>Premise 4</td>
        </tr>
        <tr>
            <td>6</td>
            <td>$\lnot D(x) \lor C(x, f_C(x))$</td>
            <td>Premise 4</td>
        </tr>
        <tr>
            <td>7</td>
            <td>$\lnot P(p) \lor \lnot B(p) \lor R(f_O(p)) \lor G(f_O(p))$</td>
            <td>Premise 5</td>
        </tr>
        <tr>
            <td>8</td>
            <td>$\lnot P(p) \lor \lnot B(p) \lor O(p, f_O(p))$</td>
            <td>Premise 5</td>
        </tr>
        <tr>
            <td>9</td>
            <td>$\lnot P(p) \lor \lnot P(q) \lor \lnot O(q, x) \lor \lnot H(p, x) \lor \lnot W(p, q)$</td>
            <td>Premise 6</td>
        </tr>
        <tr>
            <td>10</td>
            <td>$\lnot G(x) \lor \lnot O(ROBIN, x)$</td>
            <td>Negated conclusion</td>
        </tr>
        <tr>
            <td>11</td>
            <td>$W(ROBIN, YOU)$</td>
            <td>Negated conclusion</td>
        </tr>
        <tr>
            <td>12</td>
            <td>$P(ROBIN)$</td>
            <td>Given 1</td>
        </tr>
        <tr>
            <td>13</td>
            <td>$P(YOU)$</td>
            <td>Given 2</td>
        </tr>
	</tbody>
</table>

### Standardised clauses:

<table>
	<thead>
		<th>ID</th>
		<th width=600px>Clause</th>
		<th>Source ID</th>
	</thead>
	<tbody>
        <tr>
            <td>1</td>
            <td>$D(d)$</td>
            <td>Premise 1</td>
        </tr>
				<tr>
            <td>2</td>
            <td>$O(YOU, d)$</td>
            <td>Premise 1</td>
        </tr>
        <tr>
            <td>3</td>
            <td>$B(ROBIN)$</td>
            <td>Premise 2</td>
        </tr>
        <tr>
            <td>4</td>
            <td>$\lnot P(x_1) \lor \lnot R(x_2) \lor \lnot O(x_1, x_2) \lor \lnot R(x_3) \lor \lnot C(x_4, x_3) \lor H(x_1, x_4)$</td>
            <td>Premise 3</td>
        </tr>
        <tr>
            <td>5</td>
            <td>$\lnot D(x_5) \lor R(f_C(x_5))$</td>
            <td>Premise 4</td>
        </tr>
        <tr>
            <td>6</td>
            <td>$\lnot D(x_6) \lor C(x_6, f_C(x_6))$</td>
            <td>Premise 4</td>
        </tr>
        <tr>
            <td>7</td>
            <td>$\lnot P(x_7) \lor \lnot B(x_7) \lor R(f_O(x_7)) \lor G(f_O(x_7))$</td>
            <td>Premise 5</td>
        </tr>
        <tr>
            <td>8</td>
            <td>$\lnot P(x_8) \lor \lnot B(x_8) \lor O(x_8, f_O(x_8))$</td>
            <td>Premise 5</td>
        </tr>
        <tr>
            <td>9</td>
            <td>$\lnot P(x_9) \lor \lnot P(x_{10}) \lor \lnot O(x_{10}, x_{11}) \lor \lnot H(x_9, x_{11}) \lor \lnot W(x_9, x_{10})$</td>
            <td>Premise 6</td>
        </tr>
        <tr>
            <td>10</td>
            <td>$\lnot G(x_{12}) \lor \lnot O(ROBIN, x_{12})$</td>
            <td>Negated conclusion</td>
        </tr>
        <tr>
            <td>11</td>
            <td>$W(ROBIN, YOU)$</td>
            <td>Negated conclusion</td>
        </tr>
        <tr>
            <td>12</td>
            <td>$P(ROBIN)$</td>
            <td>Given 1</td>
        </tr>
        <tr>
            <td>13</td>
            <td>$P(YOU)$</td>
            <td>Given 2</td>
        </tr>
	</tbody>
</table>

### Proof by resolution

<table>
	<thead>
		<th>ID</th>
		<th>Clauses</th>
		<th width=210px>Unifier</th>
		<th width=500px>Resolution</th>
	</thead>
	<tbody>
		<tr>
			<td>14</td>
			<td>{7, 10}</td>
			<td>{ $f_O(x_7)/x_{12}$, $ROBIN/x_7$ }</td>
			<td>
				$\lnot P(ROBIN) \lor \lnot B(ROBIN) \lor R(f_O(ROBIN)) \lor \lnot O(ROBIN, f_O(ROBIN))
			$</td>
		</tr>
		<tr>
			<td>15</td>
			<td>{4, 5}</td>
			<td>{ $x_4/x_5$, $f_C(x_4)/x_3$ }</td>
			<td>
				$\lnot P(x_1) \lor \lnot R(x_2) \lor \lnot O(x_1, x_2) \lor \lnot C(x_4, f_C(x_4)) \lor H(x_1, x_4) \lor \lnot D(x_4)$
			</td>
		</tr>
		<tr>
			<td>16</td>
			<td>{6, 15}</td>
			<td>{ $x_4/x_6$ }</td>
			<td>
				$\lnot P(x_1) \lor \lnot R(x_2) \lor \lnot O(x_1, x_2) \lor H(x_1, x_4) \lor \lnot D(x_4)$
			</td>
		</tr>
		<tr>
			<td>17</td>
			<td>{9, 16}</td>
			<td>{ $x_1/x_9$, $x_4/x_{11}$ }</td>
			<td>
				$\lnot P(x_1) \lor \lnot R(x_2) \lor \lnot O(x_1, x_2) \lor \lnot D(x_4) \lor \lnot P(x_{10}) \lor \lnot O(x_{10}, x_4) \lor \lnot W(x_1, x_{10})$
			</td>
		</tr>
		<tr>
			<td>18</td>
			<td>{14, 17}</td>
			<td>{ $x_2/f_O(x_1)$, $ROBIN/x_1$ }</td>
			<td>
				$\lnot P(ROBIN) \lor \lnot D(x_4) \lor \lnot P(x_{10}) \lor \lnot O(x_{10}, x_4) \lor \lnot W(ROBIN, x_{10})$
			</td>
		</tr>
		<tr>
			<td>19</td>
			<td>{12, 18}</td>
			<td>None</td>
			<td>
				$\lnot D(x_4) \lor \lnot P(x_{10}) \lor \lnot O(x_{10}, x_4) \lor \lnot W(ROBIN, x_{10})$
			</td>
		</tr>
		<tr>
			<td>20</td>
			<td>{1, 19}</td>
			<td>{ $d/x_4$ }</td>
			<td>
				$\lnot P(x_{10}) \lor \lnot O(x_{10}, d) \lor \lnot W(ROBIN, x_{10})$
			</td>
		</tr>
		<tr>
			<td>21</td>
			<td>{13, 20}</td>
			<td>{ $YOU/x_{10}$ }</td>
			<td>
				$\lnot O(YOU, d) \lor \lnot W(ROBIN, YOU)$
			</td>
		</tr>
		<tr>
			<td>22</td>
			<td>{2, 21}</td>
			<td>None</td>
			<td>
				$\lnot W(ROBIN, YOU)$
			</td>
		</tr>
		<tr>
			<td>23</td>
			<td>{11, 22}</td>
			<td>None</td>
			<td>
				{ $\text { }$ }
			</td>
		</tr>
	</tbody>
</table>

We see that with the above sequence of steps and with the right unifiers, we were able to negate the selected clauses completely, i.e. we obtained a contradiction. This implies that, since the negated conclusion is clearly false given the contradiction, the conclusion is true. More specifically, the following hypothetical is true:

_"If the person you are looking for, i.e. Robin, does not own a grocery store, she will not date you."_

Hence, you have a shot at getting a date with Robin if she does own a grocery store; whether or not she does own one is not given.

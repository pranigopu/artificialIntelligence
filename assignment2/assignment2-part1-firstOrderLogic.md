# ECS759P: _Artificial Intelligence_<br>Assignment 2, Question 1

## Key points

- $T$ stands for $True$; for an expression $P$, $P=T$ means $P$ is true
- $F$ stands for $False$; for an expression $P$, $P=F$ means $P$ is false

## Statements & conclusion

**Statements**:

- You have a dog
- The person you are looking for buys carrots by the bushel
- Anyone who owns a rabbit hates anything that chases any rabbit
- Every dog chases some rabbit
- Anyone who buys carrots by the bushel owns either a rabbit or a grocery store
- Someone who hates something owned by another person will not date that person

**Conclusion**:

- If the person you are looking for does not own a grocery store, she will not date you

---

**Interpretations of some phrases**...

- "Own" means the same as "Have"
- "Anyone who owns a rabbit hates anything that chases any rabbit" means for all $x$, if $x$ is a rabbit & $y$ chases $x$, then the person hates $y$
- "Anyone who buys... " means " All people who buy... "
- "Someone who hates..." means "All people who hate..."
- "The person you are looking for" means "ROBIN"

Note that we interpret "the person you are looking for" as "ROBIN" is because the premises hold true for individual named Robin (i.e. "ROBIN"), and the final conclusion is a hypothetical involving the person for whom the premises hold true.

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

**Functions**:

- $f_O(x)$ _or_ `f_O(x)`: Function defined as:

```c
f_O(x):
	for all y such that O(x, y)=T do
			if R(y)=T or G(y)=T then
				return y // Return a rabbit or grocery store owned by x
			end if
		end for
	return any y such that O(x, y)=T // Return anything owned by x
```

- $f_C(x)$ _or_ `f_C(x)`: Function defined as:

```c
f_C(x):
	for all y such that C(x, y)=T do
		if R(y)=T then
			return y // Return a rabbit chased by x
		end if
	end for
	return any y such that C(x, y)=T // Return anything chased by x
```

**NOTE ON IMPLEMENTING THE ABOVE FUNCTIONS**:<br>The function $f_O$ can be implemented if (1) the set of all things owned by $x$ is known and feasibly sized or (2) the mapping between possible owners and any one thing they own is available. In short, $f_O$ is defined such that ir returns an object chased by $x$ and, if possible, returns the rabbit or grocery store object that is owned by $x$. Similarly, the function $f_C$ may not be implementable directly in the form above, but it can be implemented if (1) the set of all things chased by $x$ is known and feasibly sized or (2) the mapping between possible rabbit chasers and any one thing they chase is available. In short, $f_C$ is defined such that it returns an object chased by $x$ and, if possible, returns the rabbit object that is chased by $x$.

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

For each conversion process, we shall have the following steps:

- RI: Remove implication
- MN: Minimise negations
- SE: Skolemise existentials
- DU:  Drop universals
- CNF: Convert to CNF


### Premise 1

$\exists x \text{ } D(x) \land O(YOU, x)$

Let $DOG$ be any object such that $D(DOG) \land O(YOU, DOG)=T$

<table>
	<thead>
		<tr><th width=50px></th><th width=500px></th></tr>
	</thead>
	<tbody>
		<tr>
			<td>RI</td>
			<td>Nothing to do</td>
		</tr>
		<tr>
			<td>MN</td>
			<td>Nothing to do</td>
		</tr>
		<tr>
			<td>SE</td>
			<td>$D(DOG) \land O(YOU, DOG)$</td>
		</tr>
		<tr>
			<td>DU</td>
			<td>Nothing to do</td>
		</tr>
		<tr>
			<td>CNF</td>
			<td>Nothing to do</td>
		</tr>
	</tbody>
</table>

### Premise 2

$B(ROBIN)$

<table>
	<thead>
		<tr><th width=50px></th><th width=500px></th></tr>
	</thead>
	<tbody>
		<tr>
			<td>RI</td>
			<td>Nothing to do</td>
		</tr>
		<tr>
			<td>MN</td>
			<td>Nothing to do</td>
		</tr>
		<tr>
			<td>SE</td>
			<td>Nothing to do</td>
		</tr>
		<tr>
			<td>DU</td>
			<td>Nothing to do</td>
		</tr>
		<tr>
			<td>CNF</td>
			<td>Nothing to do</td>
		</tr>
	</tbody>
</table>

### Premise 3

$\forall p \text{ } \forall z \text{ } (P(p) \land \exists x \text{ } (R(x) \land O(p, x)) \text{ } \land \exists y \text{ } (R(y) \land C(z, y)) \rightarrow H(p, z))$

<table>
	<thead>
		<tr><th width=50px></th><th width=500px></th></tr>
	</thead>
	<tbody>
		<tr>
			<td>RI</td>
			<td>
				$\forall p \text{ } \forall z \text{ } (\lnot (P(p) \land \exists x \text{ } (R(y) \land O(p, y)) \text{ } \land \exists y \text{ } (R(y) \land C(z, y))) \lor H(p, z))$
			</td>
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
		</tr>
		<tr>
			<td>SE</td>
			<td>Nothing to do</td>
		</tr>
		<tr>
			<td>DU</td>
			<td>
				$\lnot P(p) \lor \lnot R(x) \lor \lnot O(p, x) \lor \lnot R(y) \lor \lnot C(z, y) \lor H(p, z)$
			</td>
		</tr>
		<tr>
			<td>CNF</td>
			<td>Nothing to do</td>
		</tr>
	</tbody>
</table>

### Premise 4

$\forall x \text{ } (D(x) \rightarrow \exists y \text{ } (R(y) \land C(x, y)))$

<table>
	<thead>
		<tr><th width=50px></th><th width=500px></th></tr>
	</thead>
	<tbody>
		<tr>
			<td>RI</td>
			<td>
				$\forall x \text{ } (\lnot D(x) \lor \exists y \text{ } (R(y) \land C(x, y)))$
			</td>
		</tr>
		<tr>
			<td>MN</td>
			<td>Nothing to do</td>
		</tr>
		<tr>
			<td>SE</td>
			<td>
				$\forall x \text{ } (\lnot D(x) \lor (R(f_C(x)) \land C(x, f_C(x))))$
			</td
		</tr>
		<tr>
			<td>DU</td>
			<td>
				$\lnot D(x) \lor (R(f_C(x)) \land C(x, f_C(x)))$
			</td>
		</tr>
		<tr>
			<td>CNF</td>
			<td>
				$(\lnot D(x) \lor R(f_C(x))) \land (\lnot D(x) \lor C(x, f_C(x)))$
			</td>
		</tr>
	</tbody>
</table>

### Premise 5

$\forall p \text{ } (P(p) \land B(p) \rightarrow \exists x \text{ } ((R(x) \lor G(x)) \land O(p, x)))$

<table>
	<thead>
		<tr><th width=50px></th><th width=500px></th></tr>
	</thead>
	<tbody>
		<tr>
			<td>RI</td>
			<td>
				$\forall p \text{ } (\lnot (P(p) \land B(p)) \lor \exists x \text{ } ((R(x) \lor G(x)) \land O(p, x)))$
			</td>
		</tr>
		<tr>
			<td>MN</td>
			<td>
				$\forall p \text{ } ((\lnot P(p) \lor \lnot B(p)) \lor \exists x \text{ } ((R(x) \lor G(x)) \land O(p, x)))$
			</td>
		</tr>
		<tr>
			<td>SE</td>
			<td>
				$\forall p \text{ } ((\lnot P(p) \lor \lnot B(p)) \lor ((R(f_O(p)) \lor G(f_O(p))) \land O(p, f_O(p))))$
			</td>
		</tr>
		<tr>
			<td>DU</td>
			<td>
				$(\lnot P(p) \lor \lnot B(p)) \lor ((R(f_O(p)) \lor G(f_O(p))) \land O(p, f_O(p)))$
			</td>
		</tr>
		<td>CNF</td>
			<td>
				$(\lnot P(p) \lor \lnot B(p)) \lor ((R(f_O(p)) \lor G(f_O(p))) \land O(p, f_O(p)))$
				<br>
				$\equiv (\lnot P(p) \lor \lnot B(p) \lor R(f_O(p)) \lor G(f_O(p))) \land (\lnot P(p) \lor \lnot B(p) \lor O(p, f_O(p)))$
			</td>
		</tr>
	</tbody>
</table>

### Premise 6

$\forall p \text{ } \forall q \text{ } (P(p) \land P(q) \land \exists x \text{ } (O(q, x) \land H(p, x)) \rightarrow \lnot W(p, q))$

<table>
	<thead>
		<tr><th width=50px></th><th width=500px></th></tr>
	</thead>
	<tbody>
		<tr>
			<td>RI</td>
			<td>
				$\forall p \text{ } \forall q \text{ } (\lnot(P(p) \land P(q) \land \exists x \text{ } (O(q, x) \land H(p, x))) \lor \lnot W(p, q))$
			</td>
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
		</tr>
		<tr>
			<td>SE</td>
			<td>Nothing to do</td>
		</tr>
		<tr>
			<td>DU</td>
			<td>
				$\lnot P(p) \lor \lnot P(q) \lor (\lnot O(q, x) \lor \lnot H(p, x)) \lor \lnot W(p, q)$
				<br>
				$\equiv \lnot P(p) \lor \lnot P(q) \lor \lnot O(q, x) \lor \lnot H(p, x) \lor \lnot W(p, q)$
			</td>
		</tr>
		<tr>
			<td>CNF</td>
			<td>Nothing to do</td>
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
            <td>$D(DOG) \land O(YOU, DOG)$</td>
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
		</tr>
		<tr>
			<td>MN</td>
			<td>
				$\forall x \text{ } \lnot (G(x) \land O(ROBIN, x)) \land W(ROBIN, YOU)$
				<br>
				$\equiv \forall x \text{ } (\lnot G(x) \lor \lnot O(ROBIN, x)) \land W(ROBIN, YOU)$
			</td>
		</tr>
		<tr>
			<td>SE</td>
			<td>Nothing to do</td>
		</tr>
		<tr>
			<td>DU</td>
			<td>
				$(\lnot G(x) \lor \lnot O(ROBIN, x)) \land W(ROBIN, YOU)$
			</td>
		</tr>
		<tr>
			<td>CNF</td>
			<td>Nothing to do</td>
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
            <td>$D(DOG) \land O(YOU, DOG)$</td>
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
            <td>$D(DOG)$</td>
            <td>Premise 1</td>
        </tr>
				<tr>
            <td>2</td>
            <td>$O(YOU, DOG)$</td>
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
            <td>$D(DOG)$</td>
            <td>Premise 1</td>
        </tr>
				<tr>
            <td>2</td>
            <td>$O(YOU, DOG)$</td>
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
			<td>{ $DOG/x_4$ }</td>
			<td>
				$\lnot P(x_{10}) \lor \lnot O(x_{10}, DOG) \lor \lnot W(ROBIN, x_{10})$
			</td>
		</tr>
		<tr>
			<td>21</td>
			<td>{13, 20}</td>
			<td>{ $YOU/x_{10}$ }</td>
			<td>
				$\lnot O(YOU, DOG) \lor \lnot W(ROBIN, YOU)$
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

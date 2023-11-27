## Question 1

### Statements & conclusion

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
- "Anyone who owns a rabbit hates anything that chases any rabbit" means for all x, if x is a rabbit & z chases x, then the person hates z
- "Anyone who buys... " means " All people who buy... "
- "Someone who hates..." means "All people who hate..."

### Definitions

- $Own(x, y)$: True if $x$ owns $y$
- $Hate(x, y)$: True if $x$ hates $y$
- $Chase(x, y)$: True if $x$ chases $y$
- $Bushel(x)$: True if $x$ buys carrots by bushel
- $WillDate(x, y)$: True if $x$ will date $y$
- $Dog(x)$: True if $x$ is a dog
- $Rabbit(x)$: True if $x$ is a rabbit
- $Person(x)$: True if $x$ is a person
- $Carrot(x)$: True if $x$ is a carrot
- $GroceryStore(x)$: True if $x$ is a grocery store
- $f(x)$: A function defined below:

```
f(x):
	for all y such that Rabbit(y)=T do
		if Chase(x, y) then
			return y
		end if
	end for
	return any y such that Rabbit(y)=T // Return any rabbit
```

**NOTE**: The above function may not be implementable directly in the form above, but it can be implemented if (1) the set of all rabbits is known and feasibly sized or (2) the mapping between possible rabbit chasers and any one rabbit they chase is available. They key takeaway is that $f$ is defined such that it returns a rabbit object and, if possible, returns the rabbit object that is chased by the given argument object $x$.

### Part 1

1. $Dog(x) \land Own(YOU, x)$
2. $Bushel(ROBIN)$
3. $\forall p \text{ } \forall z \text{ } \exist x \text{ } (Person(p) \land Rabbit(x) \land Rabbit(y) \land Own(p, y) \land Chase(z, x) \rightarrow Hate(p, z))$
4. $\forall x \text{ } \exists y \text{ } (Dog(x) \land Rabbit(y) \land Chase(x, y))$
5. $\forall p \text{ } (Person(p) \land Bushel(p) \rightarrow Own(p, x) \land(Rabbit(x) \lor GroceryStore(x)))$
6. $\forall p \text{ } (Person(p) \land Person(q) \land Own(q, x) \land Hate(p, x) \rightarrow \lnot WillDate(p, q))$

**NOTE**: If something is true for all, then it is also true for some and for one.

### Part 2

Transforming the statements to conjunctive normal form (CNF), i.e. a conjunct of disjuncts (product of sums, i.e. "AND of OR's").

**NOTE 1**: We can remove the universal quantifier safely when there are no variables with existential quantifiers to which the universally quantified variable maps to.

**NOTE 2**: When replacing the existential quantifier with a function $f$ of a universally quantified variable $x$, we use the same function $f$ throughout the premises, because the existential quantifier means at least one object is such that the condition involving $x$ holds true. $f$ is defined so that it maps each possible value of $x$ to a particular object accordingly.

1.
$Dog(x) \land Own(YOU, x) \equiv (Dog(x)) \land (Own(YOU))$

2.
$Bushel(ROBIN)$ (already in CNF)

3.
$\forall p \text{ } \forall z \text{ } \exists x \text{ } (Person(p) \land Rabbit(x) \land Rabbit(y) \land Own(p, y) \land Chase(z, x) \rightarrow Hate(p, z))$
_... replacing the existential quantifier with a function of the universally quantified variable..._
$\equiv Person(p) \land Rabbit(f(z)) \land Rabbit(y) \land Own(p, y) \land Chase(z, f(z)) \rightarrow Hate(p, z)$
_... removing universal quantifier..._
$\equiv Person(p) \land Rabbit(f(z)) \land Rabbit(y) \land Own(p, y) \land Chase(z, f(z)) \rightarrow Hate(p, z)$
_... replacing_ $P \rightarrow Q$ _with_ $\lnot P \lor Q$ _..._
$\equiv \lnot(Person(p) \land Rabbit(f(z)) \land Rabbit(y) \land Own(p, y) \land Chase(z, f(z))) \lor Hate(p, z)$
_... applying De Morgan's law..._
$\equiv (\lnot Person(p) \lor \lnot Rabbit(f(z)) \lor \lnot Rabbit(y) \lor \lnot Own(p, y) \lor \lnot Chase(z, f(z))) \lor Hate(p, z)$
_... rearranging parantheses..._
$\equiv (\lnot Person(p) \lor \lnot Rabbit(f(z)) \lor \lnot Rabbit(y) \lor \lnot Own(p, y) \lor \lnot Chase(z, f(z)) \lor Hate(p, z))$

4.
$\forall x \text{ } \exists y \text{ } (Dog(x) \land Rabbit(y) \land Chase(x, y))$
_... replacing the existential quantifier with a function of the universally quantified variable..._
$\equiv \forall x \text{ } (Dog(x) \land Rabbit(f(x)) \land Chase(x, f(x)))$
_... removing universal quantifier..._
$\equiv (Dog(x) \land (Rabbit(f(x))) \land (Chase(x, f(x)))$

5.
$\forall p \text{ } (Person(p) \land Bushel(p) \rightarrow Own(p, x) \land(Rabbit(x) \lor GroceryStore(x)))$
_... removing universal quantifier..._
$\equiv Person(p) \land Bushel(p) \rightarrow Own(p, x) \land (Rabbit(x) \lor GroceryStore(x))$
_... replacing_ $P \rightarrow Q$ _with_ $\lnot P \lor Q$ _..._
$\equiv \lnot(Person(p) \land Bushel(p)) \lor (Own(p, x) \land (Rabbit(x) \lor GroceryStore(x)))$
_... applying De Morgan's law..._
$\equiv (\lnot Person(p) \lor \lnot Bushel(p)) \lor (Own(p, x) \land (Rabbit(x) \lor GroceryStore(x)))$
_... distributivity..._
$\equiv (\lnot Person(p) \lor \lnot Bushel(p) \lor Own(p, x)) \land (\lnot Person(p) \lor \lnot Bushel(p) \lor Rabbit(x) \lor GroceryStore(x))$

For convenience, we shall do the following assignments:

- $P$ as $\lnot Person(p) \lor \lnot Bushel(p)$
- $Q$ as $Own(p, x) \lor Rabbit(x)$
- $R$ as $Own(p, x) \lor GroceryStore(x)$

Hence, our expression becomes:

$P \lor (Q \land R)$
_... distributivity..._
$\equiv (P \lor Q) \land (P \lor R)$
_... replacing the substitutions..._
$\equiv (\lnot Person(p) \lor \lnot Bushel(p) \lor Own(p, x) \lor Rabbit(x)) \land (\lnot Person(p) \lor \lnot Bushel(p) \lor Own(p, x) \lor GroceryStore(x))$

6.
$\forall p \text{ } (Person(p) \land Person(q) \land Own(q, x) \land Hate(p, x) \rightarrow \lnot WillDate(p, q))$
_... removing universal quantifier..._
$\equiv Person(p) \land Person(q) \land Own(q, x) \land Hate(p, x) \rightarrow \lnot WillDate(p, q)$
_... replacing_ $P \rightarrow Q$ _with_ $\lnot P \lor Q$ _..._
$\equiv \lnot (Person(p) \land Person(q) \land Own(q, x) \land Hate(p, x)) \lor \lnot WillDate(p, q)$
_... applying De Morgan's law..._
$\equiv (\lnot Person(p) \lor \lnot Person(q) \lor \lnot Own(q, x) \lor \lnot Hate(p, x)) \lor \lnot WillDate(p, q)$
_... rearranging parantheses..._
$\equiv (\lnot Person(p) \lor \lnot Person(q) \lor \lnot Own(q, x) \lor \lnot Hate(p, x) \lor \lnot WillDate(p, q))$

Standardising the variables so that each clause's variables are unique to it:

- Premise 1:<br>$(Dog(d_1)) \land (Own(YOU, d_1))$
- Premise 2:<br>$Bushel(ROBIN)$ (nothing to standardise)
- Premise 3:<br>$(\lnot Person(p_1) \lor \lnot Rabbit(f(x)) \lor \lnot Rabbit(r_1) \lor \lnot Own(p_1, r_1) \lor \lnot Chase(x, f(x)) \lor Hate(p_1, x))$
- Premise 4:<br>$(Dog(d_2)) \land (Rabbit(f(d_2))) \land (Chase(d_2, f(d_2)))$
- Premise 5:<br>$(\lnot Person(p_2) \lor \lnot Bushel(p_2) \lor Own(p_2, r_2)) \land (\lnot Person(p_2) \lor \lnot Bushel(p_2) \lor Rabbit(r_2) \lor GroceryStore(r_2))$
- Premise 6:<br>$(\lnot Person(p_3) \lor \lnot Person(p_4) \lor \lnot Own(p_4, z) \lor \lnot Hate(p_3, z) \lor \lnot WillDate(p_3, p_4))$

### Part 3

First-order logic formulation of the conclusion:

$\lnot (GroceryStore(a) \land Own(ROBIN, a) \rightarrow \lnot WillDate(ROBIN, YOU)$

Negation of the above and converting the negation to CNF:

_... negation of the above..._
$\lnot(\lnot (GroceryStore(a) \land Own(ROBIN, a)) \rightarrow \lnot WillDate(ROBIN, YOU))$
_... replacing_ $P \rightarrow Q$ _with_ $\lnot P \lor Q$ _..._
$\equiv \lnot (\lnot \lnot (GroceryStore(a) \land Own(ROBIN, a)) \lor \lnot WillDate(ROBIN, YOU))$
_... eliminating double negative..._
$\equiv \lnot ((GroceryStore(a) \land Own(ROBIN, a)) \lor \lnot WillDate(ROBIN, YOU))$
_... applying De Morgan's law..._
$\equiv \lnot (GroceryStore(a) \land Own(ROBIN, a)) \land \lnot \lnot WillDate(ROBIN, YOU)$
_... eliminating double negative..._
$\equiv \lnot (GroceryStore(a) \land Own(ROBIN, a)) \land (WillDate(ROBIN, YOU))$
_... applying De Morgan's law..._
$\equiv (\lnot GroceryStore(a) \lor \lnot Own(ROBIN, a)) \land (WillDate(ROBIN, YOU))$

### Part 4

Proof by resolution is one where, given that the premises are true, we assume the negative of the conclusion is true and look for a contradiction. If we find the contradiction, we know that the negative of the conclusion is false, thus proving the conclusion itself.

Hence, $(\lnot GroceryStore(a) \lor \lnot Own(ROBIN, a)) \land (WillDate(ROBIN, YOU))=T$

#### Proof initialisation

The following are given, i.e. taken as true:

- The conclusion
- All 6 premises
- $Person(ROBIN)$
- $Person(YOU)$

---

#### STEP 1
##### Statements

- $(\lnot GroceryStore(a) \lor \lnot Own(ROBIN, a)) \land (WillDate(ROBIN, YOU))$

##### Resolutions

- Resolution 1: $\lnot Own(ROBIN, a) \lor \lnot GroceryStore(a)$
- Resolution 2: $WillDate(ROBIN, YOU)$

---

#### STEP 2
##### Statements

- Premise 2: $Bushel(ROBIN)$
- Premise 5: $(\lnot Person(p_2) \lor \lnot Bushel(p_2) \lor Own(p_2, r_2)) \land (\lnot Person(p_2) \lor \lnot Bushel(p_2) \lor Rabbit(r_2) \lor GroceryStore(r_2))$ unifier $\{ROBIN/p_2, a/r_2\}$<br>$\equiv (\lnot Person(ROBIN) \lor \lnot Bushel(ROBIN) \lor Own(ROBIN, a)) \land (\lnot Person(ROBIN) \lor \lnot Bushel(ROBIN) \lor Rabbit(a) \lor GroceryStore(a))$

##### Resolutions

 - Resolution 3: $Own(ROBIN, a) \land (Rabbit(a) \lor GroceryStore(a))$
 
##### Explanation
 
 We know that:
 
- $Person(ROBIN)=T \implies \lnot Person(ROBIN)=F$
- $Bushel(ROBIN=T \implies \lnot Bushel(ROBIN)=F$
- $\implies \lnot Person(ROBIN) \lor \lnot Bushel(ROBIN)=F$

From the above, we get:

$(\lnot Person(ROBIN) \lor \lnot Bushel(ROBIN) \lor Own(ROBIN, a)) \land (\lnot Person(ROBIN) \lor \lnot Bushel(ROBIN) \lor Rabbit(a) \lor GroceryStore(a))$
 $\equiv (F \lor Own(ROBIN, a)) \land (F \lor Rabbit(a) \lor GroceryStore(a))$
 $\equiv Own(ROBIN, a) \land (Rabbit(a) \lor GroceryStore(a))$

---

#### STEP 3
##### Statements

- Resolution 1: $\lnot Own(ROBIN, a) \lor \lnot GroceryStore(a)$
-  Resolution 3: $Own(ROBIN, a) \land (Rabbit(a) \lor GroceryStore(a))$

##### Resolutions
- Resolution 4: $Own(ROBIN, a) \land Rabbit(a)$

##### Explanation

We have that:
$\lnot Own(ROBIN, a) \lor \lnot GroceryStore(a) = T$
_... applying De Morgan's law..._
$\equiv \lnot (Own(ROBIN, a) \land GroceryStore(a)) = T$
$\implies Own(ROBIN, a) \land GroceryStore(a) = F$

Also, we have that:
$Own(ROBIN, a) \land (Rabbit(a) \lor GroceryStore(a))$
_... distributivity..._
$\equiv (Own(ROBIN, a) \land Rabbit(a)) \lor (Own(ROBIN, a) \land GroceryStore(a))$
$\equiv (Own(ROBIN, a) \land Rabbit(a)) \lor F$
$\equiv Own(ROBIN, a) \land Rabbit(a)$

---

#### STEP 4

#### Statements

- Premise 1: $(Dog(d_1)) \land (Own(YOU, d_1))$
- Resolution 4: $Own(ROBIN, a) \land Rabbit(a)$
- Premise 3: $(\lnot Person(p_1) \lor \lnot Rabbit(f(x)) \lor \lnot Rabbit(r_1) \lor \lnot Own(p_1, r_1) \lor \lnot Chase(x, f(x)) \lor Hate(p_1, x))$ unifier $\{ROBIN/p_1, a/r_1, d_1/x\}$<br>$\equiv (\lnot Person(ROBIN) \lor \lnot Rabbit(f(d_1)) \lor \lnot Rabbit(a) \lor \lnot Own(ROBIN, a) \lor \lnot Chase(d_1, f(d_1)) \lor Hate(ROBIN, d_1))$
- Premise 4: $(Dog(d_2)) \land (Rabbit(f(d_2))) \land (Chase(d_2, f(d_2)))$ unifier $\{d_1/d_2\}$<br>$\equiv (Dog(d_1)) \land (Rabbit(f(d_1))) \land (Chase(d_1, f(d_1)))$

##### Resolutions

- Resolution 4: $Own(YOU, d_1)$
- Resolution 5:  $Hate(ROBIN, d_1)$

##### Explanation

$(Dog(d_1)) \land (Own(YOU, d_1)) \implies$

- $Dog(d_1) = T$
- $Own(YOU, d_1) = T$ ... (Resolution 4)

$(Dog(d_1)) \land (Rabbit(f(d_1))) \land (Chase(d_1, f(d_1))) \implies$

- $Dog(d_1) = T$ (already obtained)
- $Rabbit(f(d_1)) = T \implies \lnot Rabbit(f(d_1)) = F$
- $Chase(d_1, f(d_1)) = T \implies \lnot Chase(d_1, f(d_1)) = F$

Also, we know that:

- $Person(ROBIN)=T \implies \lnot Person(ROBIN) = F$
- $Own(ROBIN, a) \land Rabbit(a)=T$<br>$\implies \lnot(Own(ROBIN, a) \land Rabbit(a)) = F$<br>$\implies Own(ROBIN, a) \land Rabbit(a))  \equiv \lnot Rabbit(a) \lor \lnot Own(ROBIN, a)$ (_by De Morgan's law; order  of terms does not matter_)<br>$\implies \lnot Rabbit(a) \lor \lnot Own(ROBIN, a) = F$

Hence, we have that:

$(\lnot Person(ROBIN) \lor \lnot Rabbit(f(d_1)) \lor \lnot Rabbit(a) \lor \lnot Own(ROBIN, a) \lor \lnot Chase(d_1, f(d_1)) \lor Hate(ROBIN, d_1))$
$\equiv (F \lor F \lor F \lor F \lor Hate(ROBIN, d_1))$
$\equiv Hate(ROBIN, d_1)$ ... (Resolution 5)

---

#### STEP 5

##### Statements

- Resolution 2: $WillDate(ROBIN, YOU)$
- Resolution 4: $Own(YOU, d_1)$
- Resolution 5:  $Hate(ROBIN, d_1)$
- Premise 6: $(\lnot Person(p_3) \lor \lnot Person(p_4) \lor \lnot Own(p_4, z) \lor \lnot Hate(p_3, z) \lor \lnot WillDate(p_3, p_4))$ unifier $\{ROBIN/p_3, YOU/p_4, d_1/z\}$<br>$\equiv (\lnot Person(ROBIN) \lor \lnot Person(YOU) \lor \lnot Own(YOU, d_1) \lor \lnot Hate(ROBIN, d_1) \lor \lnot WillDate(ROBIN, YOU))$

##### Resolutions

- Contradiction

##### Explanation

We have that:

- $WillDate(ROBIN, YOU)=T \implies \lnot WillDate(ROBIN, YOU)=F$
- $Own(YOU, d_1)=T \implies \lnot Own(YOU, d_1)=F$
- $Hate(ROBIN, d_1)=T \implies \lnot Hate(ROBIN, d_1)=F$
- $Person(ROBIN)=T \implies \lnot Person(ROBIN)=F$
- $Person(YOU)=T \implies \lnot Person(YOU)=F$

Hence, we get:

$(F \lor F \lor F \lor F \lor F) \equiv F$
 
 The above shows that the given premise (premise 6) is false, but we have taken all premises to be true. Hence, we get a contradiction.

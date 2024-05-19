
# Logic

[sets](sets.md) </br>
[index](index.md)

<details> <summary>Order of operations</summary>




1. $\neg$ 
2. $\land$ 
3. $\lor$
4. $\rightarrow$
5. $\leftrightarrow$

</summary> </details>

<details> <summary>Symbols</summary>

- $A \land B == A . B == A \times B == AB$
 $A \oplus B == \lnot AB + \lnot BA$

Symbol | LaTex | meaning
-------|-------|-------
$\land$ | land | logical and
$\forall$ | forall | for every member in set
$\lor$ | lor | logical or
$\oplus$ | oplus | xor
$\exists$ | exists | there exists at least one
$\exists!$ | exists! | there exists only one
$\nexists$ | nexists | there is no


Symbol | LaTex | meaning
-------|-------|-------

![logic-gates](logic-gates.png) </br>





</summary> </details>




<details> <summary>Boolean Identities</summary>


Name | Identity
-----|---------
Additive | x + 0 x
x.0 = 0 | 
x + 1 = 1
x * 1 = x
x * x = x
x * x = x
x + !x = 1
x * !x = 0

x + yz = (x+y)(x+z)



</summary> </details>


<details> <summary>Predicate Logic</summary>

- Useful for more generalized statements </br>
P(x): x is an odd number </br>
P(2) = F </br>
$\forall x P(x) = F$ </br>



<hr>

#### Convert english into predicate logic expression
1. Read and try to understand the sentence
2. Find the domain in the statement
3. Find the quantfiers in the statement
4. Rewrite the statement so that the domain and quantifiers are visible
5. Write the statement with variables


</summary> </details>



<details> <summary>Inference rules</summary>


Inference| Another | how to remember
----|--------------|-------------------
Simplification </br> $p \land q$ </br> $\therefore p$ </br> $\therefore q$| Conjunction </br> $p$</br>  $q$ </br> $\therefore p \land q$ </br> | Simplification - S for Separate  </br> Conjunction - Conjoin the premesis with $\land$
Modus ponens </br> $p$ </br>  $p \rightarrow q$ </br> $\therefore q$ </br> | Modus tollens </br> $\neg q$ </br> $p \rightarrow q$ </br> $\therefore \neg p$ </br>
Hypothetical syllogism </br> $p \rightarrow q$ </br> $q \rightarrow r$ </br> $\therefore p \rightarrow r$ </br> | Disjunctive syllogism </br> $p \lor q$ </br> $\neg p$ </br> $\therefore q$ </br>
Addition </br> p </br> $\therefore p \lor q$ </br> | Resolution </br> $p \lor q$ </br> $\neg p \lor r$ </br> $\therefore q \lor r$



<hr>







Type | Generalization | Instantiation
-----|----------------|------
Universal | $\forall x (x \subset y)$ </br> $\therefore (x \subset)$
Existential | $\exists_x S(x)$ </br> s(neptune)


</summary> </details>









Generalized Product Rule </br>
- In every race someone must come first, second, third, fourth, etc.
- One person cannot occupy two of these positions
- The total number of race orders is N! where N is the number of runners


$$\frac{x_1 \cdot x_2 \cdot x_3 \cdot ... x_n}{n}$$



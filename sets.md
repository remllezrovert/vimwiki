# Sets

[index](index.md) </br>
[logic](logic.md) </br>



- Sets are unordered
- Sets contain only unique elements
- Two sets are called a "disjoint" if their intersection contains no values



<details> <summary>Symbols</summary>

Symbol | LaTex | Name
-------|-------|------
$\cup$ | cup | union
$\cap$ | cap | intersection
$\oplus$ | oplus | symmetric difference


Symbol | LaTex | Name
-------|-------|------
$\in$ | in | is member of 
$\ni$ | ni | owns member
$\notin$ | notin | not member of 
$\notni$ | notni | doesn't own member


- |A| means the cardinality of A
A = {2,7,5} </br>
|A| = 3 </br>



- Absolue compliment for everything in the universe outside A
    - $\bar{A}$ means the absolute compliment of A
    - A' also means "the compliment to A"

- Relative compliment (looks like a backslash)
    - A \ B = B - A
    - This is like a left outer join in SQL
- Symetric difference 
    - like a union excluding any intersecting elements





    </summary> </details>


<details> <summary>Laws</summary>

name | Identity | Identity
-----|----------|----------
DeMorgans law | $\overline{A \cap B} = \bar{A} \cup \bar{B}$| $\overline{A \cup B} = \bar{A} \cap \bar{B}$
Distributive Laws | $A \cup (A \cap B) \equiv (A \cup B) \cap (A \cup C)$
Associative Laws | $A \cup (B \cup C) \equiv (A \cup B) \cup C$
Absorbtion | $A \cup(A \cap B) \equiv A$



name | Identity | Identity
-----|----------|----------



</summary> </details>


<details> <summary>Power Sets</summary>

- The power set of set 'S' is the set of all subsets of S.
- Notation for power sets is P(S)



</summary> </details>

<details> <summary>Tuples</summary>
- Tuples allow duplicates
- Tuples use regular parenthesis ()
- Tuples are ordered
- Math tuples just like [python tuples](python-arrays.md) </br>



</summary> </details>




<details> <summary>Functions</summary>



Discrete functions 
- The codomain is often called the "target"
- Domain $\rightarrow$ Range 




#### one to one function
- $|D| \geq |T|$
- Everything in the range maps to something in the domain
- AKA Injective function 
![sets-injective](sets-injective.png)

<hr>

#### onto functions
- $|D| \leq |T|$
- $|R| = |T|$
- Everything in the codomain (target) is also in the range 
- AKA Surjective Functions
![sets-surjective](sets-surjective.png)

<hr>


Bijections
- $|D| = |T|$
- Both Surjective and Injective
- Every y value has an x
- Every target has a domain
- Reverseable mappings


Composition functions
- Applying a function to the output of another function
</summary> </details>







<details> <summary>Permutation and Combinations</summary>

####
- Both permutations and combinations do not allow repeat elements
- Every element must be distinct

#### Permutation problems involve:
- common notation for permutation is P(n,n)
- ordered(Unlike combinations)
- Arrangement or ordering problems (like anagrams)
- Example: "how many ways to re-arrage the same group"
- $P(n,r) = \frac{n!}{(n-r)!}$


#### Combination problems
- Unordered (DIFFERENT FROM PERMUTATION)
$$\binom{7}{2} = \frac{7!}{2!(7-2)!}$$
$$\binom{n}{p} = \frac{n!}{p!(n-p)!}$$




### Traveling salesman 
Input a list of cities, output them in a specific order. The order of the output is the optimal route which
minimizes the walking distance for the traveling salesman.



#### R-Permutations
$$P(n,r) = n(n-1) ... (n-r + 1)$$
$$P(n,r) = \frac{n!}{(n-r)!}$$
Example "There are 100 people, and three prizes, how many ways can people get prises" </br>
Solution: $p(100,3) = \frac{100!}{(100-3)!}$ </br>
- This is a permutation because each prize is distinct and ordered




</summary> </details>


<details> <summary>Inclusion-Exclusion</summary>

$$\sum_{p=1}^{n}(-1)^{p-1} \binom{n}{p}(n - p)!$$

$$\binom{1}{n} (n-1)! - \binom{2}{n} (n - 2)!...$$


</summary> </details>







#### Relations ####







<details> <summary>Digralphs</summary>

- Reflexive property
    - every value in the set must have at least one mapping to itself
        - Example: [(a,a), (a,b), (b,b)]
    - AntiReflexive sets cannot contain values that refer to themselves
        - Example: [(b,a), (a,b)]

- Symmetric property
    - If A points to B, then B must point to A. All connections are two way.
        - Example: [(b,a), (a,b)]
    - AntiSemetric relations cannot contain semetric pairs
        - Example: [(a,b), (b,b)]

- Transitive Property
    - If 'a' points to 'b', then 'b' must point to 'a'
        - Example: [(a,b), (b,c), (c,a)]






- An edge is the arrow in the gralph
    - Head of an edge is a the arrowhead
    - tail is the end without the head
- Vertex is a node on the relation gralph
    - In-degrees of a vertex: number of edges pointing into the edge 
    - out-degrees of a vertex: the numver of edges pointint out of a edge


- walk
    - Length is the number of edges
    - Circuit is a walk in which the first vertex is the same as the last vertex
        - cycle is a type of circuit where there are no other repeated verticies, except the first and last
    - a path is a walk if no vertex is repeated within the walk

- trail
    - A special type of walk
    - No repeated edges

- path
    - Both a walk and a trail
    - a subtype of trail
    - no reapeated edges
    - no repeated verticies (node things)

</summary> </details>



- Composite relations
    - $S \circ R$ = (a,c):b such that aRb and bSc
    - $R \circ R = R^2$ The squared notations means a composite with itself
    - Self composites replace transitive relations with direct relations
    - Self composites replace symmetric relations with reflexive ones
    - Closure is like addition, or a union
        - anti-reflexive closure is impossible
        - reflexive closure is possible
        - transitive closure is possible

    - Gralph power theorm
        - Undirected gralph G
        - Self composited k times
        - $G^k$


- Transitive closures
      - A set cannot be transitive if it doesn't contain a cycle </br>
            - ex: Take the set R = {(a,b),(b,c),(c,a),(b,d),(d,e),(e,f),(f,d)} </br>
            - Start on any node, go on a journey and find it's way back home </br>
            

    - Represented by $R^+$
    - Union with the largest walk
    - Include all of the edges (arrows) from every stage in the end product
    $$R^+ = R^5 \cup R^4 \cup R^3 \cup R^2 \cup R^1$$





Induction



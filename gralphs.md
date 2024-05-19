

# Gralphs #
[index](index.md) </br>
[dsa](dsa.md) </br>



<details> <summary>Digralphs</summary>


- An edge is the arrow in the gralph
    - Head of an edge is a the arrowhead
    - tail is the end without the head
- Vertex is a node on the relation gralph
    - In-degrees of a vertex: number of edges pointing into the edge 
    - out-degrees of a vertex: the numver of edges pointint out of a edge


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

- Regular Property
    - Every vertex has the same degree




</summary> </details>





<details> <summary>Walks</summary>




    - Length is the number of edges
    - a path is a walk if no vertex is repeated within the walk

- Closed walk
    - a walk that starts and ends on the same node





#### trails ####
    - A special type of walk
    - No repeated edges


- Circuit
    - a closed trail
    - no repeated edges
    - a walk in which the first vertex is the same as the last vertex




#### Paths ####
    - no reapeated edges
    - no repeated verticies
    - Both a walk and a trail

- Cycle 
    - a closed path
    - no repeated edges
    - no reapeated verticies


#### Trees ####
- Undirected
- Contains no cycles
- Is connected


</summary> </details>





<details> <summary>Closures</summary>




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
    - Represented by $R^+$
    - Union with the largest walk
    - Include all of the edges (arrows) from every stage in the end product
    $$R^+ = R^5 \cup R^4 \cup R^3 \cup R^2 \cup R^1$$




</summary> </details>






<details> <summary>Tree Traversals</summary>


Inorder Traversal
- LVR order: left, vertex, right

Preorder Traversal
- VLR order: vertex, left, right

Postorder Traversal
- LRV order: left, right, vertex



For n nodes, there are n - 1 edges

- The LEVEL of a node is its distance from the root
- The HEIGHT of a tree is the level of the node with the highest level in the tree
- The INTERNAL node is simply any node that isn't a leaf



- A leaf of an unrooted tree is a vertex of degree 1

- A tree contains no cycles
    - $\therefore$ There is ONLY one path between any two nodes in a tree


- The 'ARY' is the maximum number of children a node can have
- In a FULL tree every node has the maximum number of possible children
- A COMPLETE tree is a type of full tree where all leafs have the same level.
    - Perfect tryangle


</summary> </details>




Connected Components
- For a set to be a 'connected component' it must contain every single connected node within the component
    - no nodes left out.
    - example: In the gralph {(a,b), (c,d), (d,e)} 
        - there is a connected component {a,b}
        - the set {c,d} is NOT a connected component because 'd' has connections that are not listed in the set
- A single isolated node in a set is technically a 'connected component' because it is connected to itself
    - example: {a}



Vertex Connectivity
- Vertex connectivity is the number of vertexes you need to remove to make the gralph disconnected
- If you need to remove 7 vertexes before connectivity is broke. That gralph is 7 vertex connected
- If the gralph is still connected after removing any 2 given verticies, then it is 3 vertex connected



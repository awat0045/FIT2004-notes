# Graph basics
A graph is a way of modelling a set of objects and the relationships between them. They consist of nodes/vertices and edges, where the nodes represent the objects themselves and the edges represent the connections between them

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/45c7871c-f996-4492-943b-a95911d03e83)

## Graph attributes
Graphs can have certain attributes that represent their connect between elements
1. **Direction:** Edges in graphs may be directed or undirected. In an undirected graph, the edges (u,v) and (v,u) are equivalent. However, in a directed graph, edges are essentially a one way street and are not the same if you reverse them.
3. **Weights:** The edges may also be weighted or unweighted. The weight typically represents the cost to travel along that edge. For example, an edge may represent a road between two towns/nodes, where the weight of that edge is the travel time.
4. **Cycles:** A cycle is an edge/set of edges that connects a vertex to itself. A graph with no cycles or multiple edges between the same pair of vertices is called a *simple graph*.

## Directed acyclic graph
A Directed acyclic graph (DAG) is a directed graph with no cycles. They are commonly used on [topological sorting](/contents/algorithms/topologicalsort.md) problems.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/9f3f9325-ad49-4d21-8a9c-4d2f19e23cf6)

# Representation of graphs
It's important to have a way to represent our graphs so that they can be used with algorithms. There are two simple ways to do this: adjacency matrices and ajacency lists.

## Adjacency matrix
An adjacency matrix is a 2D list of size V^2, where every cell of the matrix represents an edge between the vertex i and the vertex j. In an unweighted graph the edges can be represented by 1s and 0s, but in a weighted graph the cells should represent the edge weight. 

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/2144037b-352a-49c6-935d-2ee95bfd3fea)

### Time and space complexity
- The space complexity of storing an adjacency matrix is O(V^2), as we have to store a 2D array representing all possible links between the vertices
- The time complexity of checking whether two vertices is O(1) as we can directly index the entry in the adjacency matrix.
  
## Adjacency list
Adjacency matrices are good for representing dense graphs since they use a strict amount of memory proportional to the total number of edges. However, in sparse graphs this leaves a large amount of blank space whilst still using the same O(V^2) space regardless of the actual number of edges present. Alternatively, an adjacency list is a list of lists, where each list corresponding to a particular vertex stores the vertices that given vertex is adjacent to. In a weighted graph, the adjacency list will store the weights alongside the vertices.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/1e89ab6e-7929-42e1-a7a8-a6dceac6708c)


### Time and space complexity
- The space complexity is now only O(V+E) as we are just storing the vertices and the edges themselves
- The time complexity depends on the data structure used to implement the list, but if we are using a balanced binary search tree we could do our adjacency checks in O(log(E)) time.

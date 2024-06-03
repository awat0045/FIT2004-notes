# Transitive closure 
The transitive closure of a graph G is a new graph G' on the same vertices such that there is an edge (u, v ) in G' if and only if there is a path between u and v in G .

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/5f558fdb-0815-4b3b-8263-279e51c14377)

Reading the above definition, you may notice that it's pretty similar to how we solve the all-pairs shortest path problem with [Floyd-Warshall](/contents/algorithms/floydwarshall.md), as there will be an edge between u and v in the transitive closure if dist[u][v] < inf. We can save some space as we no longer care about distances, just that there is an edge between the two. This means we can store our "distances" as binary values in a bit vector, where 0 means disconnected and 1 means connected. 

## Pseudocode
```
1: function TRANSITIVE_CLOSURE(G = (V, E))
2:   connected[1..n][1..n] = false // Store using a bitvector
3:   connected[v ][v ] = true for all vertices v
4:   connected[u][v ] = true for all edges e = (u, v ) in E
5:   for each vertex k = 1 to n do
6:     for each vertex u = 1 to n do
7:       for each vertex v = 1 to n do
8:         connected[u][v ] = connected[u][v ] or (connected[u][k] and connected[k][v ])
9:   return connected[1..n][1..n]
```

## Time and space complexity
|     |Best case|Average Case|Worst Case|
|---  |---------|------------|----------|
| Time |O(V^3)|O(V^3)|O(V^3)|
|Auxiliary Space|O(V^2/w)|O(V^2/w)|O(V^2/w)|
- This is the same as regular Floyd-Warshall, however the space complexity is now divided by w, where w is the number of bits in a machine word, thanks to the fact we're storing our connected array as a bit vector 
- We can also reduce the time complexity to O(V^3/w) using bitwise operations, however that is out of the scope of this unit.

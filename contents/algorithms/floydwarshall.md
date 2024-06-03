# The all-pairs shortest path problem
The all-pairs shortest path problem is a problem in which we seek a shortest path between every pair of vertices in a graph. This can actually be solved by solving the single-source shortest path problem using every possible vertex as the source. This seems inefficient, but in sparse graphs it can be the most efficient solution.

# The Floyd-Warshall algorithm
The Floyd-Warshall algorithm is a solution to the all-pairs shortest path problem which is efficient for dense graphs. It works off the idea that a shortest path from u -> v that has at least two edges can be decomposed into two shortest path u -> k and k -> v for some intermediate vertex k. The algorithm simply iteratively increases the pool of possible intermediate vertices by adding one vertex k at a time and updating all paths that can be improved by visiting vertex k.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/78361cdf-4eae-4455-b095-8b5b4271e62b)

Above is an example of one iteration of the Floyd-Warshall algorithm. You can see that in this iteration, we are trying to find the shortest distance from B to A. We see that the distance from B to C can be improved by travelling via the intermediate vertex A (i.e B -> A -> C is shorter than B -> C), so we can update the shortest distance from B to C to 2.

## Pseudocode
```
1: function FLOYD_WARSHALL(G = (V, E))
2:   dist[1..n][1..n] = ∞
3:   dist[v ][v ] = 0 for all vertices v
4:   dist[u][v ] = w(u, v ) for all edges e = (u, v ) in E
5:   for each vertex k = 1 to n do
6:     for each vertex u = 1 to n do
7:       for each vertex v = 1 to n do
8:         dist[u][v ] = min(dist[u][v ], dist[u][k] + dist[k][v ])
9:   return dist[1..n][1..n]
```

## Time and space complexity
|     |Best case|Average Case|Worst Case|
|---  |---------|------------|----------|
| Time |O(V^3)|O(V^3)|O(V^3)|
|Auxiliary Space|O(V^2)|O(V^2)|O(V^2)|
- The time complexity is O(V^3) as there are three loops running from 1 to n doing a constant time operation at each iteration, so the overall runtime is O(V^3)
- The space complexity is O(V^2) as we store the V*V distance matrix.


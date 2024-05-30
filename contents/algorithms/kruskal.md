# Kruskal's algorithm 
Kruskal's algorithm is another algorithm for finding MSTs, like [Prim's](/contents/algorithms/prims.md). It works by utilising the [Union-Find](/contents/algorithms/unionfind.md) data structure. We start by ordering all our edges in ascending order by weight. After that, we initialise the union-find data structure with each vertex being it's own set. We then iterate through the sorted list of edges, calling union on any two vertices that won't create a cycle in the current forest. 

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/38aff005-9be0-4980-abbd-0b406b8db6fb)

An example of a partially completed Kruskal's algorithm

## Pseudocode
```
1: function KRUSKAL(G = (V,E ))
2:   sort(E , key((u, v )) = w(u, v )) // Sort edges in ascending order of weight
3:   forest = UnionFind.initialise(n)
4:   T = (V ;)
5:   for each edge (u, v ) in E do
6:     if forest.FIND(u) 6= forest.FIND(v ) then // Ignore edges that would create a cycle
7:       forest.UNION(u, v )
8:       T.add_edge(u, v )
9:   return T
```

## Time complexity
Sorting the edges of a graph takes O(E Log(E)) time (assuming merge sort or similar), and the sequence of UNION and FIND operations takes O(E Log(V)). The total time complexity is therefore O(E Log(V)), or equivalently O(E Log(V)) since log(E) = O(log(V)) in a simple graph.

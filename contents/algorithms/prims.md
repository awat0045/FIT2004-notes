# Minimum spanning trees
A minimum spanning tree is a spanning tree of a graph G that minimises the total weight of the tree. A spanning tree itself is a subset of edges in E that connect all of the vertices in V, and since it's a kind of tree it also must be acyclic. 

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/48bace2d-0f93-452b-80a3-894729965aa1)

# Prim's algorithm
Prim's algorithm is an algorithm used for finding minimum spanning trees of weighted undirected graphs. It works similarly to [Dijkstra's](/contents/algorithms/dijkstra.md) in the sense that it begins with a source vertex (however it is arbitrarily chosen) and builds a tree T, adding edges one at a time to form an MST. The edge to add at each iteration is chosen such that it is the lightest weight edge that connects the current partial spanning tree T to some vertex V not yet in the tree.

## Pseudocode
```
1: function PRIM(G = (V,E ), r )
2:   dist[1..n] = ∞
3:   parent[1..n] = null
4:   T = ({r};)
5:   dist[r ] = 0
6:   Q = priority_queue(V[1..n], key(v ) = dist[v ])
7:   while Q is not empty do
8:     u = Q.pop_min()
9:     T.add_vertex(u)
10:    T.add_edge(parent[u], u)
11:    for each edge e = (u, v ) adjacent to u do
12:      if not v ∈ T and dist[v ] > w(u, v ) then
13:      // Remember to update the key of v in the priority queue!
14:      dist[v ] = w(u, v )
15:      parent[v ] = u
16: return T
```

## Time complexity
- Comparing the pseudocode of [Dijkstra's](/contents/algorithms/dijkstra.md) and Prim's, you'll notice the only real difference is that the key used to select the next vertex is taken to be the weight of the lightest edge connecting v to the current tree, rather than the total distance from v to the source node.
- Since this doesn't affect the complexity at all, assuming we are using a binary heap to implement our priority queue the time complexity will be the same as Dijkstra's, which is O(E Log(V))

# Topological sorting
Given a directed acyclic graph (DAG) G = (V,E), a topological ordering is an ordering of the vertices such that every node appears only after all the nodes pointing to it have already appeared.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/79f560c9-b419-45d6-b701-bcd289cb640f)

## Kahn's algorithm for topological sorting
Kahn's algorithm maintains a queue of vertices that are ready to be be completed (have no incoming edges) and inserts them one by one into the topological ordering. When a vertex is inserted, the outgoing edges are removed and it's children are checked to see if they are ready to be inserted into the topological sorting.

### Pseudocode
```
1: function TOPOLOGICAL_SORT(G = (V,E ))
2:   order = empty array
3:   ready = queue of all vertices with no incoming edges
4:   while ready is not empty do
5:     u = ready.pop()
6:     order.append(u)
7:     for each edge (u, v ) adjacent to u do
8:     Remove (u, v ) from G
9:     if v has no remaining incoming edges then
10:      ready.push(v )
11:  return order
```

### Time and space complexity 
|     |Best case|Average Case|Worst Case|
|---  |---------|------------|----------|
| Time |O(V+E)|O(V+E)|O(V+E)|
|Auxiliary Space|O(V)|O(V)|O(V)|
- The time complexity is O(V+E) because we have to visit every vertex once and remove every edge once
- The space complexity is O(V) as we keep an *order* list of all the vertices after sorting and a *ready* queue of the vertices that are ready to be pushed into the topological sort.

## Topological sorting using DFS
Topological ordering can also be achieved using a DFS. The key idea is that when we perform a DFS on some vertex v, we visit all the vertices that depend on v. Therefore if during the DFS we add a vertex to an array after visiting all it's descenfants, its descendants will have already been added to the array essentially creating a reverse topological ordering.

### Pseudocode
```
1: function TOPOLOGICAL_SORT(G = (V,E ))
2:   order = empty array
3:   visited[1..n] = false
4:   for each vertex v = 1 to n do
5:     if not visited[v ] then
6:       DFS(v )
7:   return reverse(order)
8:
9: function DFS(u)
10:   visited[u] = true
11:   for each vertex v adjacent to u do
12:     if not visited[v ] then
13:       DFS(v )
14:   order.append(u)
```

### Time and space complexity 
|     |Best case|Average Case|Worst Case|
|---  |---------|------------|----------|
| Time |O(V+E)|O(V+E)|O(V+E)|
|Auxiliary Space|O(V)|O(V)|O(V)|
- The time complexity is O(V+E) sinces it's a slightly altered DFS
- The space complexity is O(V) for the same reason

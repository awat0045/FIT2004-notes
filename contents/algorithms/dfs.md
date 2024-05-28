# Depth-First Search
A depth-first traversal searches a graph by following a path as deep as possible from some starting vertex before reaching a dead end, where there are no more adjacent and unvisited vertices, then backtracking up the path, continuing to search for vertices that have yet to be explored.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/ee75d3ae-867e-41cf-9040-308ed4b5c085)

## Pseudocode
Below is the pseudocode for a basic depth first search. Note how we keep track of the visited vertices to ensure that we dont visit the same node twice and causing an infinite loop
```
1: // Driver function that calls DFS until everything has been visited
2: function TRAVERSE(G = (V,E ))
3:   visited[1..n] = false
4:   for each vertex u = 1 to n do
5:     if not visited[u] then
6:       DFS(u)
7:
8: function DFS(u)
9:   visited[u] = true
10:   for each vertex v adjacent to u do
11:     if not visited[v ] then
12:       DFS(v )
```

## Time and space complexity 
|     |Best case|Average Case|Worst Case|
|---  |---------|------------|----------|
| Time |O(V+E)|O(V+E)|O(V+E)|
|Auxiliary Space|O(V)|O(V)|O(V)|
- The time complexity is O(V+E) because we have to visit every vertex once and examine every edge at most once
- The space complexity is O(V) because we keep a list of visited vertices with a length of V

# Finding connected components with DFS
Since DFS will visit all connected components, we can run a DFS and then run another DFS on every vertex that wasn't visited by the previous DFS as it implies that it was unreachable from the source vertex and therefore not connected to the original source. Everytime we run a DFS we increment a counter by 1 as it must be a different connected component

## Pseudocode
```
1: // Driver function that finds each connected component
2: function CONNECTED_COMPONENTS(G = (V,E ))
3:   component[1..n] = null
4:   num_components = 0
5:   for each vertex u = 1 to n do
6:     if component[u] = null then
7:       num_components += 1
8:       DFS(u, num_components)
9:   return num_components, component[1..n]
10:
11: // One DFS will visit a single connected component
12: function DFS(u, comp_num)
13:   component[u] = comp_num
14:   for each vertex v adjacent to u do
15:     if component[v ] = null then
16:       DFS(v , comp_num)

```
## Time and space complexity
|     |Best case|Average Case|Worst Case|
|---  |---------|------------|----------|
| Time |O(V+E)|O(V+E)|O(V+E)|
|Auxiliary Space|O(V)|O(V)|O(V)|
- Since we are just running DFS repeatedly, the time and space complexity are the same as DFS itself.

# Cycle finding with DFS
Performing a DFS will create a DFS tree 'T' that covers every vertex in V. If DFS encounters an edge leading to an already visited vertex, it indicates a cycle. However, we have to be careful not to consider the previous vertex, p, as part of a cycle (since this alleged cycle would use the same edge twice) so we will need to alter DFS to also keep track of the previous vertex.

## Pseudocode
```
1: // Driver function that calls DFS to look for a cycle
2: function HAS_CYCLE(G = (V,E ))
3:   visited[1..n] = false
4:   for each vertex u = 1 to n do
5:     if not visited[u] and DFS(u, null) = true then
6:       return true
7:   return false
8:
9: // Returns True if a cycle was detected
10: function DFS(u, p)
11:   visited[u] = true
12:   for each vertex v adjacent to u do
13:     if visited[v ] and v 6= p then // We found a cycle!
14:       return true
15:     else if v 6= p and DFS(v , u) = true then
16:       return true
17:   return false

```

## Time and space complexity
|     |Best case|Average Case|Worst Case|
|---  |---------|------------|----------|
| Time |O(V+E)|O(V+E)|O(V+E)|
|Auxiliary Space|O(V)|O(V)|O(V)|
- Since we are just running DFS repeatedly, the time and space complexity are the same as DFS itself.

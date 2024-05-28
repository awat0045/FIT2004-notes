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

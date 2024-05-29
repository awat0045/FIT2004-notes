# Breadth-First search
Similarly to a depth-first search, a breadth-first search is a traversal algorithm that explores all vertices of a graph until all reachable vertices have been reached. However, a breadth first search does so by visiting the vertices that are k distance away from the source, before moving to ones that are k+1 away.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/b43140ab-888b-4deb-9b44-35035365423a)

## Pseudocode
```
1: function BFS(G = (V,E ), s)
2:   visited[1..n] = false
3:   visited[s] = true
4:   queue = Queue()
5:   queue.push(s)
6:   while queue is not empty do
7:     u = queue.pop()
8:     for each vertex v adjacent to u do
9:       if not visited[v ] then
10:        visited[v ] = true
11:        queue.push(v )

```

## Time and space complexity 
|     |Best case|Average Case|Worst Case|
|---  |---------|------------|----------|
| Time |O(V+E)|O(V+E)|O(V+E)|
|Auxiliary Space|O(V)|O(V)|O(V)|
- The time complexity is O(V+E) because we have to visit every vertex once and examine every edge at most once
- The space complexity is O(V) because we keep a list of visited vertices with a length of V

# Single-source shortest paths in an unweighted graph
Breadth-first search can be used for finding the shortest paths in an unweighted graph from a given starting vertex. Since BFS finds vertices by traversing to the closest vertex first, in an unweighted and undirected graph it will by default find the shortest path to any vertex, we just need to keep track of said path and it's distance from the source.

## Pseudocode
```
1: function BFS(G = (V,E ), s)
2:   dist[1..n] = ∞
3:   pred[1..n] = null
4:   queue = Queue()
5:   queue.push(s)
6:   dist[s] = 0
7:   while queue is not empty do
8:     u = queue.pop()
9:     for each vertex v adjacent to u do
10:      if dist[v ] = ∞ then
11:      dist[v ] = dist[u] + 1
12:      pred[v ] = u
13:      queue.push(v )
```

Since we are keeping track of the predecessors, we can traverse back through the predecessor array to reconstruct the shortest paths we have found.

```
1: function GET_PATH(s, u, pred[1..n])
2:   path = [u]
3:   while u 6= s do
4:     path.append(pred[u])
5:     u = pred[u]
6:   return reverse(path)
```

## Time and space complexity 
|     |Best case|Average Case|Worst Case|
|---  |---------|------------|----------|
| Time |O(V+E)|O(V+E)|O(V+E)|
|Auxiliary Space|O(V)|O(V)|O(V)|
- The time complexity is O(V+E) since it's just a slight alteration of BFS
- The space complexity is O(V) because we are keeping two arrays and a queue, however they all store data related to the number of vertices in the graph

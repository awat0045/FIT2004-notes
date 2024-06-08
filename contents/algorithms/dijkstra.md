# Edge relaxation
Edge relaxation is the process of updating a current shortest path to an even shorter path found by enforcing the triangle inequality. It essentially checks if the current calculated distance for a certain vertex could be shortened by travelling from the vertex we are currently calculating distances from. In the Dijkstra's algorithm described below, it is largely similar to step 3.

## Pseudocode 
```
1: function RELAX(e = (u, v ))
2:   if dist[v ] > dist[u] + w(u, v ) then
3:     dist[v ] = dist[u] + w(u, v )
4:     pred[v ] = u
```

# Dijkstra's algorithm
Dijkstra's algorithm is an algorithm for finding shortest paths in graphs with non-negative weights. It works by doing the following steps:
1. Set initial distances for all vertices: 0 for the source vertex, and infinity for all the other.
2. Choose the unvisited vertex with the shortest distance from the start to be the current vertex. So the algorithm will always start with the source as the current vertex.
3. For each of the current vertex's unvisited neighbor vertices, calculate the distance from the source and update the distance if the new, calculated, distance is lower.
4. We are now done with the current vertex, so we mark it as visited. A visited vertex is not checked again.
5. Go back to step 2 to choose a new current vertex, and keep repeating these steps until all vertices are visited.
6. In the end we are left with the shortest path from the source vertex to every other vertex in the graph

## Pseudocode
```
1: function DIJKSTRA(G = (V,E ), s)
2:   dist[1..n] = ∞
3:   pred[1..n] = 0
4:   dist[s] = 0
5:   Q = priority_queue(V [1..n], key(v ) = dist[v ])
6:   while Q is not empty do
7:     u = Q.pop_min()
8:     for each edge e that goes from u to a node still in the queue do
9:       // Priority queue keys must be updated if relax improves a distance estimate!
10:      RELAX(e )
11: return dist[1..n], pred[1..n]
```

## Time and space complexity
- The time complexity of Dijkstra's algorithm depends on the implementation of the priority queue, since we need to do two things in every iteration: find the next vertex with the shortest distance, and update the current distances. This means the complexity of Dijkstra's would be O(E * update + V * find)
- However, if we use a min-heap based queue, we can get Dijkstra's to work in O(E Log(V) + V Log(V)) = O(E log(V)), as the find and update functions can run in O(log(V)) time
- The auxiliary space complexity is O(V), as we have two arrays that use O(V) space, and one priority queue that uses O(V) space (depending on binary heap implementation)

# Dijkstra's improvements
Sometimes the constraints of programming languages makes it difficult to decrease the distance of an item that is already in a priority queue, which we need to do when edge relaxing. To combat this, we can implement Dijkstra's algorithm in the following way

1. Begin with only the source vertex s in the priority queue.
2. Whenever an edge is relaxed, insert the target vertex in the priority queue keyed by its
current distance estimate.
3. When a key is removed from the priority queue, check whether it is out of date, and if so,
ignore it. A key is out of date if key(u) > dist[u].

The main difference is that we allow the priority queue to contain multiple entries for the same vertex with different distance estimates, instead of updating already inserted vertices and distances.

## Pseudocode
```
1: function DIJKSTRA(G = (V,E ), s)
2:   dist[1..n] = ∞
3:   pred[1..n] = 0
4:   dist[s] = 0
5:   Q = priority_queue()
6:   Q.push(s, key = 0)
7:   while Q is not empty do
8:     u, key = Q.pop_min()
9:     if dist[u] = key then // Do not process an out-of-date entry
10:      for each edge e that is adjacent to u do
11:        if dist[v ] > dist[u] + w(u, v ) then
12:          dist[v ] = dist[u] + w(u, v )
13:          pred[v ] = u
14:          Q.push(v , key = dist[v ])
15: return dist[1..n], pred[1..n]
```
## Time complexity
- This implementation will change the complexity so that priority queue operations run in O(log(E)) size instead of O(log(V)), causing the worst case to be O(E log(V))
- This may seem worse on paper since there can be up to v^2 edges on a graph, on a simple graph we can only have half as many edges making it asymptotically equivalent to the old implementation whilst being easier to implement/

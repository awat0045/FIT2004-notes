# Bellman-Ford Algorithm
The Bellman-Ford algorithm is an application of the dynamic programming paradigm that allows us to find the shortest distance from the source node to all vertices, if there are no negative cycles that are reachable from the source. Bellman-ford still works with negative edge weights, unlike [dijkstra's](/contents/algorithms/dijkstra.md).

## Idea of the algorithm
The algorithm works by initially setting the source node distance to 0, then all other nodes to infinity. We then perform edge relaxation on every edge in the graph. However, it's possible that this relaxation has revealed a shorter distance from one previously calculated node to another, so we must repeat the algorithm. Infact, we repeat it V-1 times, as it is possible for a shortest simple path to have up to V-1 edges.

## Finding negative cycles
Negative cycles are an issue with bellman-ford, as the presence of a negative cycle may cause the shortest path to a particular vertex to become undefined since there may exist paths of arbitrarily short length. We can check for negative cycles by running one more iteration of Bellman-Ford. If any of the distances update, there must be a negative cycle, and we can update its distance estimate to -inf.

## Pseudocode
```
1: function BELLMAN_FORD(G = (V,E ), s)
2:   dist[1..n] = ∞
3:   pred[1..n] = null
4:   dist[s] = 0
5:   for k = 1 to n − 1 do
6:     for each edge e in E do
7:       RELAX(e)
8:   return dist[1..n], pred[1..n]
```

## Time and space complexity
|     |Best case|Average Case|Worst Case|
|---  |---------|------------|----------|
| Time |O(VE)|O(VE)|O(VE)|
|Auxiliary Space|O(V)|O(V)|O(V)|
- The time complexity is easy to identify, as we are checking all the edges in the graph V-1 times, resulting in an overall complexity of O(VE))
- The space complexity is also quite simple, as the only auxiliary space we are using is to store the distances between vertices, and the predecessors, both of which require O(V) space.

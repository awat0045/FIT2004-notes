# Maximum flow problem
The maximum flow problem revolves around maximising the total amount of flow that can be sent from the source node to the sink node in a network flow. Below you can see a network with max flow:

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/7e322cbf-c3d4-4ca3-92c9-3f1633aea050)


# Ford-fulkerson algorithm
The ford fulkerson algorithm is an algorithm that can solve the max flow problem. In the most simple terms, it's effectively: *While more flow can be pushed through the network, push more flow through the network*, although it's obviously a lot more nuanced than that. To understand the Ford-Fulkerson method, we first need to understand **residual networks**.

## Residual networks
Given a flow network G = (V,E), the residual network Gf represents how much more flow can be sent through each edge. For example, an edge with capacity 9 and flow 4 has residual capacity 5, as 5 more units can be pushed along it. 

Additionally, the residual network contains *back edges* which are edges that flow in the opposite direction. The back edges are what allow the algorithm to undo flow by pushing it back along the edge that it came from, and along a new direction instead. For each edge (u,v) with positive flow f(u,v), there exists an edge (v,u) with residual capacity

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/b820bb59-8a32-4294-bb44-b3f5fdbe69a0)

## Augmenting paths
To increase the flow in a network, we seek *augmenting paths* which are capacitated paths in the residual network Gf. An augmenting path may contain forward or back edges, which correspond to two situations:

- Augmenting along a forward edge corresponds to pushing more flow through that edge
- Augmenting along a back edge corresponds to redirecting flow along that edge down a different path. The flow is reduced on the respective forward edge, and is moved to the remainder of the augmenting path

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/7f1e4d90-ebdd-40aa-b800-569d0ce25ef8)

The key thing to understand in the above image is that by augmenting along a back edge, we have redirected the flow that was once flowing along v3 -> v2 -> v4 -> t to flow directly from v3 -> t instead. As this flow is redirected away, the 4 units of flow that was being supplied by v2 to v3 is now being supplied to s, so that the flow along v2 -> v4 is not reduced. Since any flow that is reduced by augmenting along a back edge always gets replaced, an augmentation always increases the total value of the flow.

## Pseudocode - Ford-Fulkerson method
```
1: function MAX_FLOW(G = (V,E ),s,t )
2:   Set initial flow f to 0 on all edges
3:   while there exists an augmenting path p in the residual network Gf do
4:     Augment the flow f along the augmenting path p as much as possible
5:   return f
```

## Implementation via DFS
Below is an implementation of Ford-Fulkerson using [DFS](/contents/algorithms/dfs.md). This implementation is not show in the lectures so I won't explain it, instead refer to the FIT2004 course notes to understand more
```
Algorithm 60 Ford-Fulkerson implemented using depth-first search
1: // DFS returns the capacity of the augmenting path found (or 0 if there are none left)
2: function DFS(u, t , bottleneck)
3:   if u = t then return bottleneck // We hit the sink, so we have an augmenting path
4:   visited[u] = true
5:   for each edge e = (u, v ) adjacent to u do
6:     residual = e .capacity - e .flow
7:     if residual > 0 and not visited[v] then
8:       augment = DFS(v , t , min(bottleneck, residual))
9:       if augment > 0 then // We found an augmenting path - add the flow
10:        e .flow += augment
11:        e .reverse.flow -= augment
12:        return augment
13:  return 0 // We could not find an augmenting path
14:
15: function MAX_FLOW(G = (V,E ),s,t )
16:  flow = 0
17:  do
18:    visited[1..n] = false
19:    augment = DFS(s,t ,∞)
20:    flow += augment
21:  loop while augment > 0
22:  return flow
```

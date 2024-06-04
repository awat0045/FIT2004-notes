# Bipartite graphs
A bipartite graph is one where the vertices can be separated into two disjoint subsets L and R such that every edge connects a vertex u ∈ L to a vertex v ∈ R.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/764f9464-a469-4ee0-9eb2-704d42ac6bc8)

# Maximum bipartite matching
Given a bipartite graph B = (V,E), a **matching** is a subset M of the edges E such that no vertex v ∈ V is incident to multiple edges in M. A maximum matching is the max amount of edges that connect individual vertices from one subset to another without multiple edges going to the same vertex.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/0d0c1b29-c42d-46dd-8c0b-cf7fa350867f)

This can actually be solved by constructing a corresponding flow network and finding the max flow. We simply create a source vertex and connect it to all vertices in the left subset, and then we create a sink/target vertex that all the vertices in the right subset will flow into. We also have to make the edges connecting L and R directed from L to R. Then we assign all edges a capacity of 1. When we run a max flow algorithm, such as [ford fulkerson](/contents/algorithms/fordfulkerson.md) we will see that it finds the maximum bipartite matching for us.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/64d794f9-dd09-4aea-9aed-2f019343284b)

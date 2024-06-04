# The minimum cut problem
Given a flow network G = (V,E), the minimum cut problem is the problem of finding a set of edges of minimum total capacity that if removed would disconnect the source from the sink. 

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/55aafb4f-b666-43f4-b297-eee02cfbd9e3)

In the above image, the minimum cut would be removing the edges v1 -> v3, v4 -> v3, v4 -> t for a total cost of $23.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/757d321a-65eb-4e3c-956a-801788ff93b1)

# The Min-cut Max-flow Theorem
The Min-cut Max-flow theorem states that the maximum flow through any network from a given source to a given sink is exactly the sum of the edge weights that, if removed, would totally disconnect the source from the sink. In other words, for any network graph and a selected source and sink node, the max-flow from source to sink = the min-cut necessary to separate source from sink.

The Min-Cut Max-flow theorem can therefore be used to prove the correctness of ford-fulkerson (see below)
![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/7d9d248c-8ec3-4fb4-a1f0-809bb3235c6d)

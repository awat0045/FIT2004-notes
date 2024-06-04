# Circulations with Demands
Circulation with demands is a generalisation of a max-flow problem that we can use to solve combinatorial problems.  

In the problem of circulation with demands, there is no single source or sink. Instead, all vertices can potentially have both incoming and outgoing edges, and each vertex u has an assosciated number du that denotes its condition:
- If du > 0 then the vertex u has a demand of du units of flow
- If du < 0, then the vertex u has a supply of -d units of flow
- If du = 0, then the vertex u wants to keep the balance between incoming and outgoing flow in its edges.

The circulation with demands problem is to determine the feasibility of satisfying these constraints. A necessary condition for obtaining a feasible solution is that the sum of all our demands must = 0. 
![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/9e82dffc-7169-4679-a644-7fde83bbea0a)
![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/e4a63ff3-00e9-4267-bcf1-18af02a73f24)

## Reducing the problem to a max-flow problem 
To reduce the circulation with demands problem to a standard max-flow problem, there is a few steps we must do first. We create a supergraph G' of G, solve a max-flow probem in G' to obtain a solution f'max, and translate the solution f'max of the max-flow problem in G' to a solution to the circulation with demands {du} problem in G. The supergraph G' is created from G as follows: 

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/3ce2470c-6972-4dc8-bab9-e27fcfe18b97)


We then solve the max-flow problem using ford-fulkerson algorithm to get the following

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/63e9bfb4-0438-4e45-96b0-2251b06932e1)

If there is a feasible circulation f with demands {du } in G , then by setting

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/c349c242-1126-4a27-983e-4da72a21a23f)

we obtain a flow f' in G' of value D

## Pseudocode
Take note of lines 2 and 5, as both of these allow us to check if the problem is feasible or unfeasible (may be useful in exam)
![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/f2b0f867-51f7-4dfe-a42e-3d176f70f1e2)

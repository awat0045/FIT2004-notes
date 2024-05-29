# The Union-Find/Disjoint-set Data Structure
The union-find data structure is a data structure for maintaining a collection of n elements, each of which belongs to a single set, that allows us to merge the contents of some pairs of sets together. Each set is identified by a *representative* which is an arbitrary element of that set. Think of it as a key. 

## Operations
1. **Find(u)** Returns the representative of the set containing u
2. **Union(u,v)** Joins the sets containing u and v into one set. Involves changing representative of the sets

## Disjoint set forests
A disjoint set forest is a forest of sets, where each node represents an element and the root node of the set tree is the representative. The representative is indicated by it's parent pointer pointing to itself

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/5763f232-a5c1-497f-b16f-d840149ca8c3)

### Pseudocode 
```
1: function INITIALISE(n)
2:   parent[1..n] = 1..n
3:
4: function FIND(x )
5:   if parent[x ] = x then return x
6:   else return FIND(parent[x ])
7:
8: function UNION(x , y )
9:   parent[FIND(x )] = FIND(y )
```

### Time complexity
- With this unoptimised implementation, *find* will run in linear time, as we will have to follow all the parent pointers in the tree to return the representative.

## Optimising with path compression
Path compression can minimise the time it takes for us to traverse to the root. Instead of linearly searching throughout all nodes to return to the root, we can modify the parent pointer for each node on the path to point directly at the root, so longer paths are compressed and won't have to be traversed again.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/2d206b0e-de7a-4568-b0f0-467c884e9be2)

### Pseudocode
```
1: function FIND(x )
2:   if parent[x ] 6= x then parent[x ] = FIND(parent[x ])
3:   return parent[x ]
```

### Time complexity
- It can be shown that the worst-case of performing m operations is now O(m log(n)), meaning each operation will cost at most O(log(n)), much better than the unoptimised version

## Union-by-rank
In a union by rank implementation, we maintain a rank for each tree which is an upper bound on the height of each tree. When merging two trees, we make the tree with the smaller rank the child tree. This results in more balanced trees, which we can iterate through more efficiently as they won't be as deep

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/90a1df62-54de-4092-bafd-6487515321ae)


### Pseudocode
```
1: function INITIALISE(n)
2:   parent[1..n] = 1..n
3:   rank[1..n] = 0
4:
5: function UNION(x , y )
6:   x = FIND(x )
7:   y = FIND(y )
8:   if rank[x ] < rank[y ] then
9:     parent[x ] = y
10:  else
11:    parent[y ] = x
12:    if rank[x ] = rank[y ] then
13:      rank[x ] += 1

```

### Time complexity
- Much like path compression, it can be shown that the worst-case of performing m operations is now O(m log(n)), meaning each operation will cost at most O(log(n))

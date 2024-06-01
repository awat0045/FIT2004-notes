# The unbounded Knapsack problem
Imagine there is *n* heavy items and you have a backpack that can carry up to *C* kilos of items. For each of the *n* items, you have figured out their value and weight. The unbounded knapsack problem tasks us with figuring out what items to take to maximise the total value of items in out backpack. In the unbounded knapsack problem, we can take as many of each kind of item we want.

## Identifying the subproblems
The unbounded knapsack problem is quite similar to the [coin change](/contents/algorithms/coinchange.md) problem. The decisions that we can make in the knapsack problem are the items we select, analogous to the coins we select in the coin change problem. Suppose that we are trying to fill a bag with capacity Ckg. If we choose an item with weight x kg, we are then required to fill the remaining (C − x)kg of space with the most valuable items. This substructure is optimal since we always want to use the remaining (C − x)kg optimally. This suggests that our subproblems should be the following:
MaxValue[c] = {The maximum value that we can fit in a capacity of c}
for values of c such that 0 ≤ c ≤ C .

## Pseudocode - Bottom-up unbounded knapsack
```
1: function UNBOUNDED_KNAPSACK(v[1..n], w[1..n], C )
2:   MaxValue[0..C ] = 0
3:   for c = 1 to C do
4:     for i = 1 to n do
5:       if w[i] ≤ c then
6:         MaxValue[c ] = max(MaxValue[c ], v[i] + MaxValue[c − w[i]])
7:   return MaxValue[C ]

```

# The 0-1 Knapsack problem
The 0-1 Knapsack problem is the same as the unbounded one with 1 constraint. We can only take at most 1 of each item.

## Identifying the subproblems
The 0-1 Knapsack problem has an optimal substructure similar to the unbounded version, but each item can be used only once.

Looking at the below image, if we choose the blue item (2kg), we are left with 13kg. The subproblem then is to find the maximum value achievable with the remaining 13kg using the other items, highlighting the 0-1 constraint: once an item is used, it can't be reused. Keeping track of all subsets is impractical due to the exponential number of possibilities. Instead, the order of item selection is irrelevant; taking a 2kg item followed by a 4kg item is the same as the reverse.

Thus, we track the maximum value obtainable with the first i items and capacity c: MaxValue[i, c] represents the maximum value with items 1 to i and capacity c, for all 0 ≤ c ≤ C and 0 ≤ i ≤ n. If we take item i, we then consider items 1 to i-1. For i = 0, the base case is an empty set of items.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/741eef89-cb7c-48c4-8980-216910083a58)

## Pseudocode - Bottom-up 0-1 knapsack
```
1: function KNAPSACK(w[1..n], v[1..n], C )
2:   MaxValue[0..n][0..C ] = 0
3:   for i = 1 to n do
4:     for c = 1 to C do
5:       if w[i] ≤ c then
6:         MaxValue[i][c ] = max(MaxValue[i − 1][c ], v[i] + MaxValue[i − 1][c − w[i]])
7:       else
8:         MaxValue[i][c ] = MaxValue[i − 1][c ]
9:   return MaxValue[n][C ]

```

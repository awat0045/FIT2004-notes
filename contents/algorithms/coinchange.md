# The coin change problem
Suppose we have currency with denominations c1, c2,...cn and we wish to make exactly $V. There might be many ways to make this dollar amount. The coin change problem is to find the one that uses the fewest coins possible. You may try to approach this greedily, however you quickly realise that won't work. Lets imagine our coin denonimations are $1, $5, $6, $9 and we are try to find the minimum amount of coins required to make $13. The best choice would be to choose the largest coin first right? But if we do choose the largest coin, which is $9, we will have $4 left to make up which we will have to do with 4 individual $1 coins, leaving our greedy approach to require 5 coins total. However, there is a way of doing it with just 3 coins, two $6 and one $1. To do it this way, we'll have to approach the problem dynamically.

## Identifying the subproblems
We need to break this problem down into smaller subproblems to approach it dynamically. A good way of thinking about dynamic programming is to try and break the problem into a sequence of choices that lead us between subproblems. In the coin change problem, our choice is the coin we select. Every time we select a coin, our subproblem reduces in value by the amount we just selected. If we need to make $V and we choose a coin with value $x, we are now required to make change for $(V-x). The essence of dynamic programming is then to try every possible choice and take the best one, whilst memoising computations along the way to avoid repeated computation.

## Pseudocode - Top-down coin change
```
1: function COIN_CHANGE(c[1..n], v )
2:   if v = 0 then return 0
3:   if memo[v ] = null then
4:     min_coins = ∞
5:     for i = 1 to n do
6:       if c[i] ≤ v then
7:         min_coins = min(min_coins, 1 + COIN_CHANGE(v − c [i]))
8:       memo[v ] = min_coins
9:   return memo[v ]
```

## Pseudocode - Bottom-up coin change
```
1: function COIN_CHANGE(c[1..n], V )
2:   MinCoins[0..V ] = ∞
3:   MinCoins[0] = 0
4:   for v = 1 to V do
5:     for i = 1 to n do
6:       if c[i] ≤ v then
7:         MinCoins[v ] = min(MinCoins[v ], 1 + MinCoins[v − c [i]])
8: return MinCoins[V ]
```

# Reconstructing optimal solutions
We managed to find the optimal solution to the coin change problem, however we have no way of producing a list of the coins we used to get that solution. We need to extend our algorithm to produce an optimal list of coins, and there are two ways of doing so:

## Method 1: Backtracking
The first method is to backtrack through the subproblems to figure out what choices were made that lead to the optimal solution. For example, in the coin change example given earlier, the fewest coins needed to make $13 was three, so we could backtrack through the entries of the dynamic programming table over values of i = 1 to n until we found a coin ci such that MinCoins[13 - ci] = 2. When we find such a coin, the optimal substructure of the problem tells us that this coin is optimal. We then subtract ci from 13 and repeat until we reach V = 0 at which point we know we have constructed the entire solution.

## Pseudocde - Backtracking
```
1: function GET_COINS(c[1..n], V , MinCoins[0..V ])
2:   if MinCoins[V ] =∞ then return error
3:   coins = empty list
4:   while V > 0 do
5:     for i = 1 to n do
6:       if c[i] ≤ V and MinCoins[V ] = 1 + MinCoins[V − c [i]] then // c[i] is optimal
7:         coins.append(c [i])
8:         V = V − c [i]
9:   return coins
```

## Method 2: Using a decision table
Another method is to keep a second table in addition to the memo table that records the optimal decisions that were made by each subproblem.  Once the optimal value has been found, the solution can be reconstructed by looking at the decisions made in this table.  
  
Both approaches are similar, however the first one uses less space as there is no need to keep a decision array and is therefore faster as a consequence. However it is a bit more complicated to understand and implement.
## Pseudocode - Decision table
```
1: function COIN_CHANGE(c[1..n], V )
2:   MinCoins[0..V ] = ∞
3:   OptCoin[0..V ] = null
4:   MinCoins[0] = 0
5:   for v = 1 to V do
6:     for i = 1 to n do
7:       if c[i] ≤ v then
8:         if 1 + MinCoins[v − c [i]] < MinCoins[v ] then
9:           MinCoins[v ] = 1 + MinCoins[v − c [i]]
10:          OptCoin[v ] = c[i] // Remember the best coin
11:  return MinCoins[v ]
12:
13: function GET_COINS(c[1..n], V , MinCoins[0..V ], OptCoin[0..V ])
14:   if MinCoins[V] =∞ then return error
15:   coins = empty list
16:   while V > 0 do
17:     coins.append(OptCoin[V ]) // Take the best coin
18:     V = V - OptCoin[V ]
19:  return coins
```

# The edit distance problem
The edit distance problem is a way to classify how similar or dissimilar two strings of text are. For example, the words "computer" and "commuter" are similar as we change one into the other by editing one letter.  
The number of "edits" required to transform one string into another form the basis of the edit distance metric. A single edit operation consists of one of the following 3 operations:
1. Insert a new symbol in the string
2. Delete a symbol in the string
3. Replace one of the symbols in the string with any other symbol

We can also define an optimal alignment of two strings which shows where the optimal number of edits occur. An optimal alignment for "computer" and "commuter" would involve substituting 'p' for 'm'.

## Identifying optimal sub problems
Consider the problem of finding an optical alignment for the strings “ACAATCC” and “AGCATCG”. To find the optimal alignment for these strings we consider the final column of the alignment with three choices:

1. Substitute the last 'C' for 'G':
   ```
   C
   G
   *
   ```

2. Delete the last 'C':
   ```
   C
   -
   *
   ```

3. Insert 'G' at the end:
   ```
   -
   G
   *
   ```

Each choice leads to an optimal alignment of the remaining characters. Therefore, the optimal alignment of "ACAATCC" and "AGCATCG" is one of:

- `OPTIMAL_ALIGNMENT("ACAATC", "AGCATC")` +
  ```
  C
  G
  *
  ```

- `OPTIMAL_ALIGNMENT("ACAATC", "AGCATCG")` +
  ```
  C
  -
  *
  ```

- `OPTIMAL_ALIGNMENT("ACAATCC", "AGCATC")` +
  ```
  -
  G
  *
  ```

The remaining prefixes must also be optimally aligned. Thus, we define our subproblems as:

```
Dist[i, j] = The edit distance between the prefixes S1[1..i] and S2[1..j]
```
for 0 ≤ i ≤ n, 0 ≤ j ≤ m.

## Pseudocode - Bottom-up edit distance
```
1: function EDIT_DISTANCE(S1[1..n], S2[1..m])
2:   Dist[0..n][0..m] = 0
3:   Dist[1..n][0] = 1..n
4:   Dist[0][1..m] = 1..m
5:   for i = 1 to n do
6:     for j = 1 to m do
7:       if S1[i] = S2[j] then
8:         Dist[i][j] = Dist[i-1][j-1]
9:       else
10:        Dist[i][j] = min(Dist[i-1][j-1], Dist[i-1][j], Dist[i][j-1]) + 1
11:  return Dist[n][m]
```

## Backtracking for optical alignment
The above pseudocode will return the edit distance for two strings, however it won't return the actual optimal alignment. To do so, we need to use the backtracking technique we learnt from [dynamic programming](/contents/algorithms/dynamic.md).

```
1: function ALIGNMENT(S1[1..n], S2[1..m], Dist[0..n][0..m])
2:   A1 = "", A2 = ""
3:   i = n, j = m
4:   while i + j > 0 do
5:     if i = 0 then
6:       A1 += "-", A2 += S2[j]
7:       j = j − 1
8:     else if j = 0 then
9:       A1 += S1[i], A2 += "-"
10:      i = i − 1
11:    else
12:      best = min(Dist[i − 1][j − 1], Dist[i][j − 1], Dist[i − 1][j])
13:      if S1[i] = S2[j] or Dist[i − 1][j − 1] = best then // Substitution
14:        A1 += S1[i], A2 += S2[j]
15:        i = i − 1, j = j − 1
16:      else if Dist[i − 1][j] = best then // Deletion from S1
17:        A1 += S1[i], A2 += "-"
18:        i = i − 1
19:      else // Insertion into S1
20:        A1 += "-", A2 += S2[j]
21:        j = j − 1
22:  return reverse(A1), reverse(A2)
```

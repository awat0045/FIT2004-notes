# Suffix arrays
Suffix arrays are a compact data structure that index all of the suffixes of a particular string in sorted order. A suffix array of a string is a sorted array of its suffixes, so the suffix array of banana looks like:

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/1647a964-26f0-4c74-9fa9-f99a15d5556e)

Since actually storing all of the suffixes of a string would take O(n^2)) space, suffix arrays are represented in a more compact form, where each element simply refers to an index into S where the corresponding suffix begins. For example, the suffix array for banana would be stored as: 

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/f2ae39eb-388c-442a-99d5-83f7639bb10d)

where the ith index corresponds to the position in banana at which the ith sorted suffix starts as show in the below table:

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/e2cda8de-9013-4242-b6a1-faed1665d39b)

## Building a suffix array
### The Naive Approach
The simplest way to build a suffix array is to build a list containing indices 1..n and sort them by comparing suffixes. In practice, the time complexity is O(n^2 * log(n)), owing to the fact sorting performs O(n log(n)) comparisons and each pair of suffixes takes O(n) time to compare.

#### Naive suffix array construction
```
1: function SUFFIX_ARRAY(S[1..n])
2:   SA[1..n] = [1..n]
3:   sort(SA[1..n], SUFFIX_COMPARE(S,...)) // Use suffix_compare as the comparison operator
4:   return SA
5:
6: // Compare the suffixes at position i and j
7: function SUFFIX_COMPARE(S[1..n], i, j)
8:   return (S[i..n] < S[j..n])
```

### The Prefix Doubling Algorithm
The naive algorithm is simply too slow to practically work on large strings. A faster approach is the *prefix doubling* algorithm:

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/3273d0ca-9800-48fc-8618-6adbc522de96)

If we perform prefix doubling by naively comparing substrings at each iteration, this will be no faster than the naive algorithm, so we need a trick to perform the comparisons faster.

#### Fast suffix comparison
Prefix doubling iteratively sorts longer and longer substrings each round. The key idea is that by knowing the sorted order of the shorted substrings, we can compare the longest substrings fast: 

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/89e77bb5-2701-4b7c-9f7c-1614dc0902fe)

#### Maintaing sorted order
The last issue we must discuss is keeping track of the sorted order of the suffices. We need to maintain a second array, the rank array. The rank array remembers for each suffix, its current position in the suffix array. Two suffixes that are equal up to the current length must be assigned the same rank so that we know they are equal.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/5a134a1e-8c00-4962-93e6-8f5ca2e3b36d)

If we know the ranks of two suffixes, we can compare them by simply comparing their ranks, since a lower rank means it comes earlier in the suffix array.

### Prefix-doubling suffix array construction
```
1: function SUFFIX_ARRAY(S[1..n])
2:   SA[1..n] = [1..n]
3:   rank[1..n] = [ord(S[1..n])]
4:   for k = 1 to n, stepping k ×= 2 do
5:     sort(SA[1..n], suffix_compare(rank, k, ...))
6:     // Update the rank array to account for the new sorted order
7:     temp[1..n] = 0
8:     for i = 1 to n − 1 do
9:       temp[SA[i+1]] = temp[SA[i]] + suffix_compare(rank[1..n], k, SA[i], SA[i + 1])
10:    swap(temp, rank)
11:  return SA
12:
13: // Compare the suffixes of length 2k beginning at positions i and j
14: function SUFFIX_COMPARE(rank[1..n], k, i, j)
15:   if rank[i] 6= rank[j] then // Compare by first halves
16:     return rank[i] < rank[j]
17:   else if i + k ≤ n and j + k ≤ n then // Compare by second halves
18:     return rank[i + k] < rank[j + k]
19:   else // Second half is empty
20:     return j < i
```

## Pattern matching with suffix arrays
Since suffix arrays give suffixes in sorted order, all occurrences of the pattern that we are searching for will exist in some contiguous range. Since they are sorted, we can find this range with a pair of binary searches, one to locate the first occurrence and one to locate the final occurrence. Since each string comparison takes O(m) time and the binary searches must perform O(log(n)) iterations, the total time complexity of pattern matching using a suffix array is O(m log(n))

### Pseudocode - Pattern matching with a suffix array
```
1: function FIND_PATTERN(SA[1..n], T[1..n], P[1..m])
2:   // Binary search to find the first occurrence of P
3:   // Invariant: T[SA[lo]..n] < P and T[SA[hi]..n] ≥ P
4:   lo = 0, hi = n
5:   while lo < hi - 1 do
6:     mid = b(lo + hi)/2c
7:     if T[SA[mid]..n] < P[1..m] then
8:       lo = mid
9:     else
10:      hi = mid
11:  begin = hi
12:  // Binary search to find the final occurrence of P
13:  // Invariant: T[SA[lo]..n] ≤ P and T[SA[hi]..n] < P
14:  lo = 1, hi = n + 1
15:  while lo < hi - 1 do
16:    mid = b(lo + hi)/2c
17:    if T[SA[mid]..n] ≤ P[1..m] then
18:      lo = mid
19:    else
20:      hi = mid
21:  end = lo
22:  return begin, end
```


# Merge sort
Merge sort is a divide-and-conquer comparison based sorting algorithm that sorts a given sequence by dividing it into two halves, sorting those two halves, and merging them back together. It sorts the individual halves by calling merge sort recursively, until we're left with only individual elements. From there we can merge all the individual elements in order until we're left with a sorted list

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/1907b64c-9459-410e-940c-cbf76b5b6f26)
- Diagram of the merge sort routine

## Pseudocode
Merge sort consists of two seperate algorithms: merge and merge sort. Merge works by comparing the individual elements of the two lists we're attempting to merge, and appending the smallest element of each comparison to our result list:
```
1: function MERGE(A[i..n1], B[j..n2])
2:   result = empty array
3:   while i ≤ n1 or j ≤ n2 do
4:     if j > n2 or i ≤ n1 and A[i] ≤ B[j] then
5:     result.append(A[i])
6:     i += 1
7:   else
8:     result.append(B[j])
9:     j += 1
10: return result
```

Merge sort works by repeatedly splitting the given array in half until they're individual elements, and calls merge to merge them all back together into a sorted list

```
1: function MERGE_SORT(array[lo..hi])
2:   if hi > lo then
3:     mid = b(lo + hi)/2c
4:     MERGE_SORT(array[lo..mid])
5:     MERGE_SORT(array[mid + 1..hi])
6:     array[lo..hi] = MERGE(array[lo..mid], array[mid + 1..hi])
```

## Time and space complexity
|     |Best case|Average Case|Worst Case|
|---  |---------|------------|----------|
| Time |O(n log(n))|O(n log(n))|O(n log(n))|
|Auxiliary Space|O(n)|O(n)|O(n)|
- The time complexity is O(n log(n)) as merge takes O(n) time, and we are repeating it for the depth of the recurrence, which is log(n)
- The space complexity is O(n) due to the merge algorithm, which returns a *result* list of size n

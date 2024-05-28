# Quickselect
Quickselect is an algorithm that is used to find the kth smallest element in a list, also known as the kth order statistic. It works very similarly to quicksort. We start by partitioning our list around a pivot element, and, due to the nature of partitioning, we know that once we partition a list our pivot is in it's final sorted position. We then recurse into whichever side our kth smallest element will be located in and repeat until we determine it

## Pseudocode
```
1: function QUICKSELECT(array[lo..hi], k)
2:   if hi > lo then
3:     pivot = array[lo]
4:     mid = PARTITION(array[lo..hi], pivot)
5:     if k < mid then
6:       return QUICKSELECT(array[lo..mid − 1], k)
7:     else if k > mid then
8:       return QUICKSELECT(array[mid + 1..hi], k)
9:     else
10:      return array[k]
11:  else
12:    return array[k]

```

## Time complexity
|     |Best case|Average Case|Worst Case|
|---  |---------|------------|----------|
| Time |O(n)|O(n)|O(n^2)|
- Since we only have to recurse through one half of the list, the best and average cases are reduced to O(n) instead of the O(log(n)) seen in quicksort.
- However, the worst case is still O(n^2) which will happen if we select the minimum or maximum element repeatedly.

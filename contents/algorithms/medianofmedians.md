# Median of medians
The key idea of median of medians is to find an approximate median in linear time. The use for finding a median in linear time is that we can implement it to find a good pivot in quicksort, reducing the worst case complexity from O(n^2) to O(n log(n)), because our pivots will no longer be the largest or smallest element in the array. 

Median of medians selects an approximate median by doing the following:
- Dividing the original list of n elements into (n/5) groups of size at most 5
- Finding the median of these groups (just sort them as they are small)
- Finding the true median of the n/5 medians using quickselect

## Pseudocode
```
1: function MEDIAN_OF_MEDIANS(array[lo..hi])
2:   if hi - lo < 5 then
3:     return MEDIAN_OF_FIVE(array[lo..hi])
4:   else
5:     medians = empty array
6:     for i = lo to hi, step 5 do
7:       j = min(i + 4, hi)
8:       median = MEDIAN_OF_FIVE(array[i..j])
9:       medians.append(median)
10:   n = length(medians)
11:   return QUICKSELECT(medians[1..n], b(n + 1)/2c)
12:
13: function MEDIAN_OF_FIVE(array[lo..hi])
14:   INSERTION_SORT(array[lo..hi]
15:   return array[(lo + hi)/2]
```

## Time complexity
- Median of medians has a worst case complexity of O(n)

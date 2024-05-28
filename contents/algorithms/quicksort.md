# Quicksort 
Quicksort is a divide and conquer comparison based sorting algorithm, similar to merge sort. Quick sort works by choosing a pivot and partitioning an array around said pivot, so all elements smaller than the pivot are on the left, and all elements larger are on the right. We then repeat the process on the left and right sides recursively, until the entire list is sorted.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/cf588110-7198-4fe6-97b1-02479e40c8e8)

## Pseudocode
```
1: function QUICKSORT(array[lo..hi])
2:   if hi > lo then
3:     pivot = array[lo]
4:     mid = PARTITION(array[lo..hi], pivot)
5:     QUICKSORT(array[lo..mid − 1])
6:     QUICKSORT(array[mid + 1..hi])
```

## Time and space complexity 
|     |Best case|Average Case|Worst Case|
|---  |---------|------------|----------|
| Time |O(n log(n))|O(n log(n))|O(n^2)|
|Auxiliary Space|O(log(n))|O(log(n))|O(log(n)|

The running time of quicksort is dependent on the quality of pivot chosen. Ideally the resulting partition will be balanced which will reduce the recursive depth of the function. 
- The best case partition is when the pivot is the median of the array, so our array will half in size every iteration. This means we will partition the array in O(n) time, log(n) times resulting in the O(n log(n)) complexity.
- In the worst case, our pivot will either be the smallest or largest item in the array as the array size will only be reduced by one at every iteration, resulting in a recursive depth of O(n) and an overall complexity of O(n^2)
- However, on average, the partitions obtained by an arbitrary pivot will neither be a perfect median or the smallest or largest element. This means the splits will be "okay" on average, resulting in the O(n log(n)) complexity as the chances of us choosing the smallest or largest element every iteration are incredibly slim

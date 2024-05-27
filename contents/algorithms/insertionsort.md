# Insertion sort
Insertion sort is similar to selection sort in the sense that it keeps two sublists: sorted and unsorted. However, insertion sort works by selecting the first element in the unsorted list, then compares it to the elements in the sorted list until it finds the correct location to insert

## Pseudocode
```
1: function INSERTION_SORT(array[1..n])
2:   for i = 2 to n do
3:     key = array[i]
4:     j = i - 1
5:     while j > 0 and array[j] > key do
6:       array[j + 1] = array[j]
7:       j = j - 1
8:     array[j + 1] = key
```

## Time and space complexity

|     |Best case|Average Case|Worst Case|
|---  |---------|------------|----------|
| Time |O(n)|O(n^2)|O(n^2)|
|Auxiliary Space|O(1)|O(1)|O(1)|
- The worst case complexity will happen when the list is in reverse sorted order. We have to iterate through the outer and inner for loop n times, as every item will be in the wrong position
- The best case will occur if the list is already sorted. We will just iterate through the outer for loop, checking that every item is in the correct position

## Stability
Insertion sort is stable, as we will insert duplicate elements after the original element

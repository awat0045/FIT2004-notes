# Partitioning
The aim of partitioning is to sort a list into 3 segments: smaller than the pivot, equal to the pivot and larger than the pivot. Partitioning is integral to the quicksort algorithm, and the choice of partitioning algorithm affects the time and space complexity of quicksort.

## Naive partition algorithm
The naive partitioning algorithm partitions the input array into 3 temporary arrays: one with elements less than the pivot, one with elements equal to the pivot, and one with elements greater than the pivot

### Pseudocode
```
1: function PARTITION(array[lo..hi], pivot)
2:   left = empty array // Store elements less than the pivot
3:   pivots = empty array // Store elements equal to the pivot
4:   right = empty array // Store elements greater than the pivot
5:   for i = lo to hi do
6:     if array[i] < pivot then left.append(array[i])
7:     else if array[i] = pivot then pivots.append(array[i])
8:     else right.append(array[i])
9:   array[lo..hi] = left + pivots + right // Concatenate the arrays
10:   return length(left) + length(pivots)/2
```

### Time and space complexity
- Naive partitioning takes O(n) time and is stable
- However, it is not in place as it stores all n elements in new arrays, taking up O(n) space
- The creation of extra arrays also means it will be slower in practice than the alternatives

## Hoare partition algorithm
The Hoare partition algorithm works by maintaining two indices at each end of the array. The two indices then move towards each other, swapping any element that is on the wrong side of the pivot

### Pseudocode
```
1: function PARTITION(array[lo..hi], array[p]) // array[p] is a reference to the pivot element
2:    swap(array[lo], array[p]) // Move the pivot to the front of the array
3:     i = lo, j = hi
4:     while i ≤ j do
5:       while i ≤ j and array[i] ≤ array[p] do i = i + 1
6:       while i ≤ j and array[j] > array[lo] do j = j − 1
7:       if i ≤ j then swap(array[i], array[j]) // swap elements on the wrong side
8:     swap(array[lo], array[j]) // swap the pivot into the correct position
9:     return j
```
### Time and space complexity
- Takes O(n) time like naive partitioning, however it is no longer stable
- It is in-place as all operations are done on the input list

## Dutch National Flag partitioning
One disadvantage of the hoare partitioning algorithm is that it can perform badly when there are many elements equal to the pivot. All elements equal to the pivot will end up on the left side of the pivot, causing it to become unbalanced and affecting the efficiency of quicksort. 

The dutch national flag algorithm aims to solve this issue by sorting the list into 3 sections represented by red, white and blue. Red items are smaller than the pivot, white elements equal to the pivot and blue elements larger than the pivot.

We use 3 pointers to maintain the invariant of the DNF problem which is that:
- array[1..lo − 1] contains the red items
- array[l o..mid − 1] contains the white items
- array[mid..hi] contains the currently unknown items
- array[hi + 1..n] contains the blue items

We initially set lo = 1, mid = 1, hi = n so that the whole list is initially in the unknown section. We then iteratively move items from the unknown section into their corresponding sections whil updating the pointers. At each iteration we move the item at array[mid]. There are 3 cases to consider when doing this:

**Case 1: array[mid] is Red:**
If array[mid] is red, it needs to move to the first section, so we'll swap array[mid] with array[lo] and increment the lo pointer by 1

**Case 2: array[mid] is white:** 
If array[mid] is white, then its already in the correct position so we just increment the mid pointer

**Case 3: array[mid] is blue**
If array[mid] is blue, we need to move it to the final section. To do so we will swap array[mid] with array[hi] and decrement the hi pointer.

### Pseudocode
```
1: function PARTITION(array[1..n], pivot)
2:   lo = 1, mid = 1, hi = n
3:   while mid ≤ hi do
4:     if array[mid] < pivot then // Red case
5:       swap(array[mid], array[lo])
6:       lo += 1, mid += 1
7:     else if array[mid] = pivot then // White case
8:       mid += 1
9:     else // Blue case
10:      swap(array[mid], array[hi])
11:      hi -= 1
12:   return lo, mid
```



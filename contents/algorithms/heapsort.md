# Heapsort
Heapsort works by using a binary heap data structure. The binary heap data structure can be described as follows:
- A binary heap is a complete binary tree (all levels except for the last are completely filled)
- Every element in a max heap is no smaller than it's children (i.e. the maximum element is at the top of the heap)
![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/c5cfbe45-0fc3-44fc-9c35-44a9e318c6cf)

There are some key properties of a binary heap that allow heapsort to work
- Due to it's structure, a binary heap can be represented as a flat array *array[1..n]* where the root node is array[1] and for each node *array[i]* it's children are elements *array[2i]* and *array[2i+1]*
- We can convert an array to a heap (heapify) in O(n) time
- A new item can be inserted into a binary heap in O(log(n)) time.
- The maximum element can be removed from a binary heap in O(log(n)) time.

## Pseudocode for heapsort
Because of the above mentioned properties of binary heaps, it's incredibly simple to perform heapsort. We just heapify the array, and successively remove the largest element and place it at the back of the array
```
1: function HEAPSORT(array[1..n])
2:   HEAPIFY(array[1..n])
3:   for i = n to 1 do
4:     array[i] = EXTRACT_MAX(array[1..i])
```

## Time and space complexity of heapsort
|     |Best case|Average Case|Worst Case|
|---  |---------|------------|----------|
| Time |O(n)|O(n log(n))|O(n log(n))|
|Auxiliary Space|O(1)|O(1)|O(1)|

- The best case is O(n) which happens when we our input array consists of all identical elements so extract_max takes constant time
- The worst case is O(n log(n)), as we have to remove the max element, which takes O(log(n)) time, and we have to do that n times for all the elements in the input array
- The algorithm is in-place as all the operations are performed on the input list itself

## Pseudocode for assosciated operations
### Heapify
```
1: function HEAPIFY(array[1..n])
2:   for i = n/2 to 1 do
3:     FALL(array[1..n], i)
```

### Heap: Insert
```
1: function INSERT(array[1..n], x )
2:   array.append(x )
3:   n += 1
4:   RISE(array[1..n], n)
```

### Heap: Delete
```
1: function EXTRACT_MAX(array[1..n])
2:   swap(array[1], array[n])
3:   n = n - 1
4:   FALL(array[1..n], 1)
5: return array.pop_back()
```

### Heap: Rise
```
1: function RISE(array[1..n], i)
2:   parent = i/2
3:   while parent ≥ 1 do
4:     if array[parent] < array[i] then
5:       swap(array[parent], array[i])
6:       i = parent
7:       parent = i/2
8:     else
9:       break
```

### Heap: Fall
```
1: function FALL(array[1..n], i)
2:   child = 2i
3:   while child ≤ n do
4:     if child < n and array[child+1] > array[child] then
5:       child += 1
6:     if array[i] < array[child] then
7:       swap(array[i], array[child])
8:       i = child
9:       child = 2i
10:   else
11:     break
```

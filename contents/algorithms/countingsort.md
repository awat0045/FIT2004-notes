# Counting sort
Counting sort is an efficient way of sorting integers. We simply count the number of times an integer occurs, then re-insert those integers in an array in the correct order. However this would not be stable, so we need to do a second pass over the input and place each element in the correct position. We will keep a seperate array, called position to do so, and use the following sum to determine the start position of element y.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/dd2e1fa9-1ea5-473a-9cc7-2fc344cf31cb)

## Pseudocode
```
1: function COUNTING_SORT(array[1..n], u)
2:   counter[0..u − 1] = [0, 0,...]
3:   for i = 1 to n do
4:     counter[array[i]] += 1
5:   position[0..u − 1] = [1, 0,...]
6:   for v = 1 to u − 1 do
7:     position[v ] = position[v − 1] + counter[v − 1]
8:   temp[1..n] = [0, 0,...]
9:   for i = 1 to n do
10:   temp[position[array[i]] = array[i]
11:   position[array[i]] += 1
12:  swap(array, temp) 
```

## Time and space complexity
|     |Best case|Average Case|Worst Case|
|---  |---------|------------|----------|
| Time |O(n + u)|O(n + u)|O(n + u)|
|Auxiliary Space|O(n + u)|O(n + u)|O(n + u)|

- We are required to create and maintain the counter array of size u, and we do two passes over the input, resulting in the time and space complexity of O(n + u)

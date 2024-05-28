# Radix sort
There are many types of radix sorts, however we'll focus on the Least significant digit (LSD) version. It works by sorting an array of elements one digit at a time, from the least significant (furtherst right) to the most significant. Each digit must be sorted in a stable manner to maintain the relative ordering of the previously sorted digits. Since each digit has a small range of possible values (0-9) we will use a stable counting sort.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/0c8c4d0a-942e-47b3-9aaf-a4f57436c875)

## Pseudocode
```
1: function RADIX_PASS(array[1..n], base, digit)
2:   counter[0..base-1] = [0,0,...],
3:   for i = 1 to n do
4:     counter[GET_DIGIT(array[i], base, digit)] += 1
5:   position[0..base-1] = [1,0,...]
6:   for v = 1 to base −1 do
7:     position[value] = position[v − 1] + counter[v − 1]
8:   temp[1..n] = [0,0,...]
9:   for i = 1 to n do
10:    digit = GET_DIGIT(array[i],base,digit)
11:    temp[position[digit]] = array[i]
12:    position[digit] += 1
13: swap(array, temp)
14:
15: function RADIX_SORT(array[1..n], base, digits)
16:   for digit = 1 to digits do
17:     RADIX_PASS(array[1..n], base, digit)
```

## Time and space complexity 
|     |Best case|Average Case|Worst Case|
|---  |---------|------------|----------|
| Time |O(k(n+b))|O(k(n+b))O(k(n+b))|
|Auxiliary Space|O(n + b)|O(n + b)|O(n + b)|
- The time complexity comes from us doing a counting sort k number of times, where k is the number of digits in our numbers
- The space complexity is just that of counting sort

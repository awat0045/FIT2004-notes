# Fibonacci sequence
The fibonacci sequence is a well known algorithm where the next number in the sequence is the sum of the previous two numbers. It can be easily implemented recursively, as seen below.

## Pseudocode - Recursive fibonacci
```
1: function FIBONACCI(n)
2:   if n ≤ 1 then
3:     return n
4:   else
5:     return FIBONACCI(n-1) + FIBONACCI(n-2)
```

However, using what we know about [dynamic programming](/contents/algorithms/dynamic.md) and memoisation, is there a more efficient way of implementing this?

# Memoised fibonacci numbers
The fibonacci sequence has a large amount of repeated calculations. For example, to calculate f(4) we will need to sum f(2) and f(3). We have already calculated f(2) by this point in the sequence, so there is no need for us to recalculate it. Instead, we can store the result of f(2) when we first calculate it, and access it from the memo array when we need it in the future.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/d0fd60a3-ad0e-4295-b348-2658c3f56529)

## Pseudocode - Top-down Fibonacci numbers
```
1: function FIBONACCI_MEMO(n)
2:   if n ≤ 1 then return n // The base case
3:   if memo[n] = null then // Compute it for the first time
4:     memo[n] = FIBONACCI_MEMO(n − 1) + FIBONACCI_MEMO(n − 2)
5:   return memo[n]
6:
7: function FIBONACCI(n)
8:   memo[0..n] = null
9:   return FIBONACCI_MEMO(n)

```

## Pseudocode - Bottom-up Fibonacci numbers
```
1: function FIBONACCI(n)
2:   fib[0..n] = 0
3:   fib[1] = 1
4:   for i = 2 to n do
5:     fib[i] = fib[i − 1] + fib[i − 2]
6:   return fib[n]
```

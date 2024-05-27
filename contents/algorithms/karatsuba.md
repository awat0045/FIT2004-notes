# Karatsuba's multiplication algorithm
Karatsuba's multiplication algorithm revolves around solving the multiplication algorithm we learnt in primary school (which runs in O(n^2) time) more efficiently. It runs more efficiently by reducing the problem into 3 instances of size n/2, instead of the primary school algorithm which reduces to 4 instances of n/2

## Pseudocode
```
1: function KARATSUBA(x , y ) . x and y are n-digits positive numbers
2:   if n = 1 then
3:     Compute x · y in one step and return the result.
4:   else
5:     Let xM and xL denote the first and second halves of x , respectively.
6:     Let yM and yL denote the first and second halves of y , respectively.
7:     Compute u = (xM + xL) using the grade school addition algorithm.
8:     Compute v = (yM + yL) using the grade school addition algorithm.
9:     a = KARATSUBA(xM , yM )
10:    b = KARATSUBA(xL, yL)
11:    c = KARATSUBA(u, v )
12:    Compute z = c − a − b using the grade school subtraction algorithm.
13:    Compute a * 10n +z * 10^(n/2) + b using left shifts and the grade school addition algorithm,
and return the result
```

## Time complexity
- Runs in O(n^1.59) time due to reducing the problem into 3 instance of size n/2

# Measures of complexity
There are 3 different ways to measure the complexity of an algorithm: best, worse and average case complexity

## Best case complexity
The *best case* complexity of an algorithm is the fewest possible instructions that the algorithm will execute over any possible input, as a function of the input size.
- Best case complexity isn't determined by it's behaviour for small inputs

## Worst case complexity
The *worst case* complexity is the most instructions that an algorithm could possibly exxecute on any possible input

## Average case complexity
The average case complexity is harder to define, however the simplest definition is that the average case complexity is the average number of operations that the algorithm will execute, averaged over all possible inputs of a given size

# Space complexity vs auxiliary space complexity
- Space complexity is the total amount of space taken by an algorithm as a function of input size
- Auxiliary space complexity is the amount of space taken by an algorithm excluding space taken by the input

## In-place algorithms
- An algorithm is considered in-place if it has O(1) auxiliary space complexity
  1. i.e it does not store or copy the input into any additional data structure, but modifies the input directly

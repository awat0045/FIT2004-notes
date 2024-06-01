# Dynamic programming
The essence of dynamic programming is to solve a problem by breaking it into smaller subproblems and combining the solutions of those subproblems into a solution to the greater problem. Dynamic programming applies when there are overlapping subproblems that repeat multiple times

## Memoisation
Memoisation is the process of remembering the solutions to previously computed subproblems and storing them in a table for later lookup. This saves us time in the scenario where the same subproblem may need to be computed multiple times, as we can just look it up in the table instead of recomputing.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/7266fcdc-6498-48aa-ac91-bd246815ac7e)

- An example of memoisation on a [fibonacci](/contents/algorithms/fibonacci.md) sequence. Notice how we don't have to recalculate repeat calculations.

## Optimal Substructure
A combinatorial problem exhibits optimal substructure if it can be broken down into smaller subproblems, such that the solutions to the subproblems can be combined to obtain a solution to the original problem.

## Top-down vs Bottom-up approach to dynamic programming
In a top-down approach we work from the top of the problem and break our problem into smaller subproblems as we travel down. In this approach the memoisation table is filled on demand as the particular subproblems are required. In a bottom-up approach, we start by solving all the individual subproblems before combining them to the final solution. In this approach, we fill the solution table one problem at a time in an order which ensures that any dependent subproblems have already been computed before they are needed

|Pros: Top-down approach|Pros: Bottom-up approach|
|---|---|
|No need to know the topological ordering of the subproblem dependencies|Avoids recursion, which is typically slower than iteration.|
|Avoids computing the solution to subproblems that are not needed|Allows for clever optimisations|
|More intuitive for programmers who like to think recursively.|Might be more intuitive for programmers who don’t like recursion.|

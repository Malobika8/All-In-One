# How to identify questions where Stack might be used?

If there exists a problem, that can be done in O(n^2) time complexity with loops, with j dependent on i, probability is that it can be solved in
a better way with Stack.

i -> 0 to n

j is either of the following:
- j -> 0 to i
- j -> i to 0
- j -> i to n
- j -> n to i


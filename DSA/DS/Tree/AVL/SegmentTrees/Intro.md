# Intro 

Segment Tree is a versatile data structure used in computer science and data structures that allows efficient querying and updating of 
intervals or segments of an array. It is particularly useful for problems involving range queries, such as finding the sum, minimum, 
maximum, or any other operation over a specific range of elements in an array. The tree is built recursively by dividing the array into 
segments until each segment represents a single element. This structure enables fast query and update operations with a time complexity of 
O(log n), making it a powerful tool in algorithm design and optimization.

It is used while working with ranges. Segment tree nodes contain query results and segments.

### Q1. Find the sum between two indices of an array.

Steps:
- If (node.startInd > segmentEndIndex || node.endInd < segmentStartIndex): return default value i.e. 0
- If (node.startInd >= segmentStartIndex && node.endInd <= segmentEndIndex): return value
- Total sum = sum from left + sum from right

### Q2. Replace value in an index and update the tree accordingly.

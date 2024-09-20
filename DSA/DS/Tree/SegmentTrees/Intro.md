# Intro 

Segment Tree is a versatile data structure used in computer science and data structures that allows efficient querying and updating of 
intervals or segments of an array. It is particularly useful for problems involving range queries, such as finding the sum, minimum, 
maximum, or any other operation over a specific range of elements in an array. The tree is built recursively by dividing the array into 
segments until each segment represents a single element. This structure enables fast query and update operations with a time complexity of 
O(log n), making it a powerful tool in algorithm design and optimization.

It is used while working with ranges. Segment tree nodes contain query results and segments.

<img width="1018" alt="Screenshot 2024-09-20 at 6 31 31 PM" src="https://github.com/user-attachments/assets/70f25282-0f41-4643-8c3b-6a420accea38">
<img width="1022" alt="Screenshot 2024-09-20 at 6 31 39 PM" src="https://github.com/user-attachments/assets/b0bd5aa8-dcba-4d7c-88cc-d7c3320a3af3">
<img width="1024" alt="Screenshot 2024-09-20 at 6 31 47 PM" src="https://github.com/user-attachments/assets/4b86d436-f086-4f9b-a847-57b500ce92bd">

### Q1. Find the sum between two indices of an array.

Steps:
- If (node.startInd > segmentEndIndex || node.endInd < segmentStartIndex): return default value i.e. 0
- If (node.startInd >= segmentStartIndex && node.endInd <= segmentEndIndex): return value
- Total sum = sum from left + sum from right

### Q2. Replace value in an index and update the tree accordingly.

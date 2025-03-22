# Important

1. Adjacency list
2. Indegree & Outdegree
3. BFS: Queue
4. DFS: Recursion
5. Topological sort using BFS: Least indegree's first. Use queue. Decrease by 1 everytime for each of the adjacent vertices. Add to queue whose indegree is 0;
6. Topological sort using DFS: Use stack and put vertices in stack while returning from recursive calls. Pop from stack one by one in the end.
7. Detect cycle in an undirected graph: Use parent concept. If next vertex is visited and parent of current vertex is not same as next vertex, there's a cycle.
8. Detect cycle in a directed graph: Simple DFS with two boolean arrays - visited & dfsvisited. If vertex is visited and dfsvisited, there's a cycle present.
9. 

# Important

1. Adjacency list
2. Indegree & Outdegree
3. BFS: Queue
4. DFS: Recursion
5. Topological sort using BFS: Least indegree's first. Use queue. Decrease by 1 every time for each of the adjacent vertices. Add to queue whose indegree is 0;
6. Topological sort using DFS: Use stack and put vertices in the  stack while returning from recursive calls. Pop from the stack one by one in the end.
7. Detect cycle in an undirected graph: Use parent concept. If the next vertex is visited and the parent of current vertex is not the same as the next vertex, there's a cycle.
8. Detect cycle in a directed graph: Simple DFS with two boolean arrays - visited & dfsvisited. If a vertex is visited and dfsvisited, there's a cycle present.
9. Detect nodes in a cycle: Have a new boolean array and track nodes if present in a cycle. (Practise eventual safe nodes (leetcode))

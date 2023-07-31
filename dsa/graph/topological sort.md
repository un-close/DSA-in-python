## Definition:
ordering of DAC graph such that all the nodes in increasing in-degree

## Implementation:

- ## DFS:
	- DFS of nodes unvisited and pushing them to a stack when the call is finished

```py
graph = [[1, 2, 3], [5], [], [], [2, 3], [2]]  
visited = [False] * len(graph)  
ordering = list()  
  
  
def dfs(node):  
    visited[node] = True  
    for neig in graph[node]:  
        if not visited[neig]:  
            dfs(neig)  
    ordering.insert(0, node)  
  
  
for i in range(len(graph)):  
    if not visited[i]:  
        dfs(i)  
print(ordering)
```

- ## Kahn's algorithm 
	- using onion peeling technique
	- can be used to check for cycle detection

```py
  
graph = [[1, 2, 3], [5], [], [], [2, 3], [2]]  
queue, in_degree, ordering, index = list(), [0] * len(graph), [-1] * len(graph), 0  
for Neighbour in graph:  
    for To in Neighbour:  
        in_degree[To] += 1  
for i in range(len(graph)):  
    if in_degree[i] == 0:  
        ordering[index] = i  
        queue.append(i)  
        index += 1  
for node in queue:  
    for neighbour in graph[node]:  
        in_degree[neighbour] -= 1  
        if in_degree[neighbour] == 0:  
            queue.append(neighbour)  
            ordering[index] = neighbour  
            index += 1  
print(ordering if index == len(graph) else 'cycle detected')
```

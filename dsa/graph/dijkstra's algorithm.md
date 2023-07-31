## Summary:
To find the shortest path between a node and all other nodes given that the graph doesn't contain any negative edges.

# INTUITION:
- greedily select the best possible path

# IMPLEMENTATION:
```python
def solve():  
    n, edges = map(int, inp().split())  
    graph = defaultdict(list)  
    for _ in range(edges):  
        fr, to, cost = map(int, inp().split())  
        graph[fr].append([to, cost])  
    heap, prev, dist, visited = list(), [None] * n, [float('inf')] * n, [False] * n  
    start = int(input('pls enter the starting node\n'))  
    end = int(input('pls enter the ending node\n'))  
    dist[start] = 0  
    heapq.heappush(heap, [0, start])  
    while heap:  
        curr_dist, node = heapq.heappop(heap)  
        if dist[node] < curr_dist:  # optimization 1  
            continue  
        visited[node] = True  
        for neig, e_cost in graph[node]:  
            if visited[neig]:  
                continue            
            if curr_dist + e_cost < dist[neig]:  
                dist[neig] = curr_dist + e_cost  
                prev[neig] = node  
                heapq.heappush(heap, [dist[neig], neig])  
        if node == end:  # optimization 2  
            break  
    path, at = list(), end  
    while at:  
        path.append(at)  
        at = prev[at]  
    path.append(start)  
    print(f'the shortest distance between {start} and {end} is :{dist[end]}')  
    print(f'the path followed is {path[::-1]}')
```

# CODE SNIPPET:
```python
def dijkstra(graph, source, destination):

    distance = {node: float('inf') for node in graph}

    distance[source] = 0

  

    queue = [(0, source)]

  

    while queue:

        current_distance, current_node = heapq.heappop(queue)

  

        if current_node == destination:

            return distance[current_node]

  

        if current_distance > distance[current_node]:

            continue

  

        for neighbor, weight in graph[current_node]:

            new_distance = current_distance + weight

  

            if new_distance < distance[neighbor]:

                distance[neighbor] = new_distance

                heapq.heappush(queue, (new_distance, neighbor))

  

    return -1  # If destination is unreachable
```
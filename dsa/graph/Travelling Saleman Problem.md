## Summary:
- find the minimum Hamiltonian path

# INTUITION:
- generate all possible paths and find the minimum distance from it.

# IMPLEMENTATION 1:
```python
def tsp1(graph, s, n):  
    path = defaultdict(list)  
    vertex, min_distance = [i for i in range(n) if i != s], float('inf')  
    next_perm: list  
  
    for next_perm in itertools.permutations(vertex):  
        curr_distance, source = 0, s  
        for i in next_perm:  
            curr_distance, source = graph[source][i] + curr_distance, i  
        curr_distance += graph[source][s]  
        path[curr_distance] = [s] + list(next_perm) + [s]  
        min_distance = min(min_distance, curr_distance)  
    print(min_distance)  
    print(path[min_distance])
```

# INTUTION:
- we can find the minimum distance for k nodes and built up from this using dynamic programming

# IMPLEMENTATION 2:

```python
import sys

def combinations(r_count, n):
    """Helper function to generate all possible combinations of r_count bit set out of n bits"""
    def backtracking(pos, r, subsets, sets):
        if n - pos < r:
            return
        if r == 0 and pos == n:
            sets.append(subsets)
        for i in range(pos, n):
            subsets |= (1 << i)  # set ith bit
            backtracking(i + 1, r - 1, subsets, sets)
            subsets &= ~(1 << i)  # unset ith bit
    backtracking(0, r_count, 0, ans := list())
    return ans

def setup(graph, table, s, n):
    """Initialize the DP table for the TSP with 2 nodes"""
    for node in range(n):
        if node != s:
            table[node][(1 << s) | (1 << node)] = graph[s][node]

def notin(i, s):
    """Helper function to check if the ith element is not in the set s"""
    return ((1 << i) & s) == 0

def solve(graph, table, s, n):
    """Solve the TSP using dynamic programming"""
    for r in range(3, n + 1):
        for sets in combinations(r, n):
            if notin(s, sets):
                continue
            for next_node in range(n):
                if next_node == s or notin(next_node, sets):
                    continue
                set_without_next = sets ^ (1 << next_node)
                local_minima = float('inf')
                for end in range(n):
                    if end == s or end == next_node or notin(end, sets):
                        continue
                    new_distance = table[end][set_without_next] + graph[end][next_node]
                    local_minima = min(local_minima, new_distance)
                table[next_node][sets] = local_minima
    end_state, min_distance = (1 << n) - 1, float('inf')
    for i in range(n):
        if i != s:
            distance = table[i][end_state] + graph[i][s]
            min_distance = min(min_distance, distance)
    print(min_distance)

def retrack(graph, table, s, n):
    """Backtrack to find the optimal path for the TSP"""
    path, state, last_index = [s], (1 << n) - 1, s
    for _ in range(1, n):
        distance, new_index = float('inf'), -1
        for i in range(n):
            if i == s and notin(i, state):
                continue
            curr_dist = table[i][state] + graph[i][last_index]
            if curr_dist < distance:
                new_index, distance = i, curr_dist
        path.append(new_index)
        state ^= (1 << new_index)
        last_index = new_index
    path.append(s)
    print(path[::-1])

def tsp2(graph, s, n):
    """Main function to solve the TSP"""
    table = [[sys.maxsize] * (1 << n) for _ in range(n)]
    setup(graph, table, s, n)
    solve(graph, table, s, n)
    retrack(graph, table, s, n)

```
# DEFINE:
-   A union-find data structure is a data structure that stores a collection of disjoint sets.
-   It provides two main operations: union (which merges two sets together) and find (which determines which set a given element belongs to).
-   The goal of a union-find data structure is to efficiently perform these operations while maintaining certain properties, such as the connectivity of the sets.
-   Union-find data structures are often used in algorithms that involve clustering or connected components, such as Kruskal's algorithm for finding a minimum spanning tree or image segmentation.
-   One popular optimization for the union-find data structure is called "union by rank with path compression", which guarantees logarithmic time complexity for both union and find operations.

# IMPLEMENTATION:
```python
import sys  
  
inp = sys.stdin.readline  
out = sys.stdout.write  
flush = sys.stdout.flush  
  
  
class DSU:  
    def __init__(self, n):  
        self.parent = list(range(n))  
        self.rank = [0] * n  
  
    def find(self, node):  
        if self.parent[node] != node:  
            self.parent[node] = self.find(self.parent[node])  
        return self.parent[node]  
  
    def union(self, a, b):  
        leader_a, leader_b = self.find(a), self.find(b)  
        if leader_a == leader_b:  
            return        
        if self.rank[leader_a] < self.rank[leader_b]:  
            self.parent[leader_a] = leader_b  
        elif self.rank[leader_a] > self.rank[leader_b]:  
            self.parent[leader_b] = leader_a  
        else:  
            self.parent[leader_b] = leader_a  
            self.rank[leader_a] += 1  
  
  
number, m = map(int, inp().split())  
dsu = DSU(number)  
for _ in range(m):  
    command, a, b = input().split()  
    if command == 'union':  
        dsu.union(int(a) - 1, int(b) - 1)  
    else:  
        res = 'YES' if dsu.find(int(a) - 1) == dsu.find(int(b) - 1) else 'NO'  
        out(f'{res}\n')  
        flush()
```
# Summary:
DSU with minimum, maximum and total no of elements present in the set.
problem link:[[B - Disjoint Sets Union - Codeforces](https://codeforces.com/edu/course/2/lesson/7/1/practice/contest/289390/problem/B)]

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
        self.min = list(range(1, n + 1))  
        self.size = [1] * n  
        self.max = list(range(1, n + 1))  
  
    def find(self, node):  
        if self.parent[node] != node:  
            self.parent[node] = self.find(self.parent[node])  
        return self.parent[node]  
  
    def union(self, a, b):  
        leader_a, leader_b = self.find(a), self.find(b)  
        if leader_a == leader_b:  
            return        
        if self.rank[leader_a] < self.rank[leader_b]:  
            self.min[leader_b] = min(self.min[leader_a], self.min[leader_b])  
            self.max[leader_b] = max(self.max[leader_a], self.max[leader_b])  
            self.parent[leader_a] = leader_b  
            self.size[leader_b] += self.size[leader_a]  
        elif self.rank[leader_a] > self.rank[leader_b]:  
            self.min[leader_a] = min(self.min[leader_a], self.min[leader_b])  
            self.max[leader_a] = max(self.max[leader_a], self.max[leader_b])  
            self.parent[leader_b] = leader_a  
            self.size[leader_a] += self.size[leader_b]  
        else:  
            self.parent[leader_b] = leader_a  
            self.min[leader_a] = min(self.min[leader_a], self.min[leader_b])  
            self.max[leader_a] = max(self.max[leader_a], self.max[leader_b])  
            self.rank[leader_a] += 1  
            self.size[leader_a] += self.size[leader_b]  
  
  
no_of_element, no_of_queries = map(int, inp().split())  
dsu = DSU(no_of_element)  
for _ in range(no_of_queries):  
    q = inp().split()  
    if q[0] == 'union':  
        dsu.union(int(q[1]) - 1, int(q[2]) - 1)  
    else:  
        leader = dsu.find(int(q[1]) - 1)  
        min_ele, max_ele, size = dsu.min[leader], dsu.max[leader], dsu.size[leader]  
        out(f'{min_ele} {max_ele} {size}\n')  
        flush()
```
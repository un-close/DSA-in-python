# Link:
[B - Frog 2 (atcoder.jp)](https://atcoder.jp/contests/dp/tasks/dp_b)

# IMPLEMENTATION:
```python
def solve():  
    n, k = map(int, inp().split())  
    cost = tuple(map(int, inp().split()))  
    stones = [float('inf')] * (n + 1)  
    stones[1] = 0  
    stones[2] = abs(cost[1] - cost[0])  
    for i in range(3, n + 1):  
        for j in range(1, min(i, k) + 1):  
            stones[i] = min(stones[i], stones[i - j] + abs(cost[i - 1] - cost[i - j - 1]))  
    print(stones[-1])
```
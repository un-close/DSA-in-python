## Summary:
- classical knapsack with weight ranging at-most $10^9$.
- [E - Knapsack 2 (atcoder.jp)](https://atcoder.jp/contests/dp/tasks/dp_e)

# INTUITION:
Maximum value that can be formed from all the item given is $10^5$. So replace the weight column of the classical knapsack problem with values from $1$ to $10^5$.

# IMPLEMENTATION:
```python
def solve():  
    items, max_capacity = map(int, inp().split())  
    query = [list(map(int, inp().split())) for _ in range(items)]  
    query.sort()  
    max_val = sum(i for _, i in query)  
    min_weighs = [[max_capacity + 1] * (max_val + 1) for _ in range(items + 1)]  
    min_weighs[0][0] = 0  
    for item in range(1, items + 1):  
        wi, vi = query[item - 1]  
        for value in range(1, max_val + 1):  
            min_weight = min_weighs[item - 1][value]  
            if value >= vi:  
                min_weight = min(min_weight, min_weighs[item - 1][value - vi] + wi)  
            min_weighs[item][value] = min_weight  
    print(max_val - next(val for val, weight in enumerate(min_weighs[-1][::-1]) if weight <= max_capacity))
```
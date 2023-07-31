### Summary:
Baxter Scott owns a dairy company with magical cows that double in number every day. The Dairy Regulator limits the number of cows on each farm. If a farm exceeds the limit, Baxter moves half of the cows to a new farm. The Regulator needs to know how many farms she will inspect, given the number of cows on each farm on a given day. Farms with zero cows are not inspected, and farms with at least one cow are inspected.

# EXPLANATION:
[(3) Magic Cows | Dynamic Programming | Adhoc | Interview problem - YouTube](https://www.youtube.com/watch?v=_tur2nPkIKo&list=PLDV1Zeh2NRsAsbafOroUBnNV8fhZa7P4u&index=2&ab_channel=WilliamFiset)

# IMPLEMENTATION:
```python
def solve():  
    c, n, m = map(int, inp().split())  
    initial_cows = [int(inp()) for _ in range(n)]  
    query = [int(inp()) for _ in range(m)]  
    days = max(query)  
    dp = [[0] * (c + 1) for _ in range(days + 1)]  
    for i in range(n):  
        dp[0][initial_cows[i]] += 1  
    for day in range(days):  
        for i in range(c + 1):  
            if i <= c // 2:  
                dp[day + 1][i * 2] += dp[day][i]  
            else:  
                dp[day + 1][i] += 2 * dp[day][i]  
    ans = [sum(dp[q]) for q in query]  
    print('\n'.join(map(str, ans)))
```
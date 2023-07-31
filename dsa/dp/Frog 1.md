# Link:
[A - Frog 1 (atcoder.jp)](https://atcoder.jp/contests/dp/tasks/dp_a)

# IMPLEMENTATION:
```python
def solve():  
    n = int(inp())  
    cost = [int(i) for i in inp().split()]  
    if n == 2:  
        print(abs(cost[-1] - cost[0]))  
        return  
    dp = [0] * (n + 1)  
    dp[2] = abs(cost[1] - cost[0])  
    for i in range(3, n + 1):  
        one_step = dp[i - 1] + abs(cost[i - 1] - cost[i - 2])  
        two_step = dp[i - 2] + abs(cost[i - 1] - cost[i - 3])  
        dp[i] = min(one_step, two_step)  
    print(dp[-1])
```
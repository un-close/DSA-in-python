# Link:
[C - Vacation (atcoder.jp)](https://atcoder.jp/contests/dp/tasks/dp_c)

# IMPLEMENTATION:
```python
def solve():  
    n = int(inp())  
    mat = list(list(map(int, inp().split())) for _ in range(n))  
    dp = [[float('-inf')] * 3 for _ in range(n)]  
    dp[0] = mat[0]  
    for i in range(1, n):  
        for j, k in product(range(3), range(3)):  
            if j != k:  
                dp[i][j] = max(dp[i][j], dp[i-1][k] + mat[i][j])  
    print(max(dp[-1]))
```
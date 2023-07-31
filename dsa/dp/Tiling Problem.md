# LINK:
[(3) Tiling problems [1/2] | Dynamic Programming - YouTube](https://www.youtube.com/watch?v=gQszF5qdZ-0&list=PLDV1Zeh2NRsAsbafOroUBnNV8fhZa7P4u&index=2&ab_channel=WilliamFiset)

### Summary:
Determine the total way of tiling a board of length n with blocks of length m, l respectively.

# INTUITION:
The question can be divided into solving the question of board of length `i`, less than n, and keep decreasing the length until we are left with the question, *how many ways can you create a board of length 0*, whose answer is 1, which is by not choosing anything. The recurrence relation for the 2 block with different length is given here by `dp[n] = dp[n-m] + dp[n-l]`.

# NAIVE IMPLEMENTATION:
```python
def recursive(n, m, l):  
    if n < 0:  
        return 0  
    if n == 0:  
        return 1  
    return recursive(n - m, m, l) + recursive(n - l, m, l)  
  
print(recursive(n, m, l))
```

# DP IMPLEMENTATION:
```python
def solve():  
    n = int(inp())  
    m, l = map(int, inp().split())  
    if m > l:  
        m, l = l, m  
    dp = [0] * (n + 1)  
    dp[m] = dp[0] = 1  
    for i in range(m, n + 1):  
        tile1 = dp[i - m] if i - m >= 0 else 0  
        tile2 = dp[i - l] if i - l >= 0 else 0  
        dp[i] = tile1 + tile2  
    print(dp[-1])
```
## Summary:
Given the Knapsack with limited capacity (given) and bunch of rocks with associated weight and value, determine the maximum value that the knapsack can have.

# NAIVE IMPLEMENTATION:
```python
def solve():  
    def knapSack(W, wt, val, n):  
        total = 1 << n 
        max_sum = 0  
        for i in range(total):  
            curr_weight = curr_sum = 0  
            for j in range(n):  
                if i & (1 << j):  
                    if curr_weight + wt[j] <= W:  
                        curr_weight += wt[j]  
                        curr_sum += val[j]  
                    else:  
                        break
            if curr_weight <= W:  
                max_sum = max(max_sum, curr_sum)  
        return max_sum  
  
    n, w = 3, 3  
    val = [1, 2, 3]  
    wt = [4, 5, 6]  
    print(knapSack(w, wt, val, n))
```


# DP approach:
The problem of choosing the optimal subset of items such that their total weight sum fits inside the knapsack and the value is maximized can be sub-divided into smaller problem of choosing `ith` item to be included into the a knapsack of `wth` capacity and finding the best value of this problem, i.e. what is the maximum value that can be made from `ith` items with knapsack of `wth` capacity. Solving this for `i = n` and `w = W` gives our answer.

```python
def knapSack_1(W, wt, val, n):  
    dp = [[0] * (W + 1) for _ in range(n + 1)]  
    for item in range(1, n + 1):  
        for curr_capacity in range(1, W + 1):  
            curr_weight, curr_val = wt[item - 1], val[item - 1]  # zero based indexing  
            prev_val = dp[item][curr_capacity] = dp[item - 1][curr_capacity]  
            if (curr_capacity - curr_weight) >= 0 and dp[item - 1][curr_capacity - curr_weight] + curr_val > prev_val:  
                dp[item][curr_capacity] = dp[item - 1][curr_capacity - curr_weight] + curr_val  
    return dp[-1][-1]  # optimal answer by considering all the n items and capacity W
```

# Space Optimized DP approach:
As u can observe above, we are only using previous row information, so we can space optimize our previous solution.

```python
def knapSack_2(W, wt, val, n):  
    dp = [[0] * (W + 1) for _ in range(2)]  
    index = 1  
    for curr_items in range(1, n+1):  
        index = 1 - index  
        for curr_capacity in range(1, W+1):  
            curr_val, curr_weight = val[curr_items-1], wt[curr_items-1]  
            dp[1 - index][curr_capacity] = dp[index][curr_capacity]  
            if curr_capacity - curr_weight > -1 and dp[index][curr_capacity - curr_weight] + curr_val > dp[1 - index][curr_capacity]:  
                dp[1 - index][curr_capacity] = dp[index][curr_capacity - curr_weight] + curr_val  
    return dp[1 - index][-1]
```

# ITEMS INCLUDED:
- **dp (version 1)** with below code:
```python
included = list()  
next_weight = W  
for item in range(n, 0, -1):  
    if dp[item][next_weight] != dp[item-1][next_weight]:  
        included.append(item)  
        next_weight -= wt[item-1]  
print(included[::-1])
```
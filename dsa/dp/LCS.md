### Summary:
Given 2 strings, find the longest common subsequence of both of them.

# NAIVE IMPLEMENTATION:

```python
def subseq(s):  
    n = len(s)  
    sub = set()  
    total = 1 << n  
    for i in range(total):  
        temp = str()  
        for j in range(n):  
            if i & (1 << j):  
                temp += s[j]  
        sub.add(temp)  
    return sub  
  
ans = ''  
s1_set, s2_set = subseq(s1), subseq(s2)  
if s_set := s1_set.intersection(s2_set):  
    for i in s_set:  
        if len(i) > len(ans):  
            ans = i  
print(ans)
```

# DP APPROACH:

```python
def dp_method(s1, s2):  
    dp = [[0] * (len(s1) + 1) for _ in range((len(s2) + 1))]  
    for i in range(1, len(s2) + 1):  
        for j in range(1, len(s1) + 1):  
            if s1[j - 1] == s2[i - 1]:  
                dp[i][j] = 1 + dp[i - 1][j - 1]  
            else:  
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])  
    ans, i, j = '', len(s2), len(s1)  
    while i or j:  
        if i and dp[i][j] == dp[i - 1][j]:  
            i -= 1  
        elif j and dp[i][j] == dp[i][j - 1]:  
            j -= 1  
        else:  
            i, j = i - 1, j - 1  
            ans += s2[i]  
    return ans[::-1]  
  
print(dp_method(s1, s2))
```
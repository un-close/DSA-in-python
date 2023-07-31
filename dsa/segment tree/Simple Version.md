# CODE:
```python
from math import gcd, lcm

class segment_tree:

    def __init__(self, n):

        self.tree = [0] * (4 * n)

        self.left = 0

        self.right = n - 1

        self.fn = max

  

    def sum_build(self, arr):

  

        def Sum(arr, node, left, right):

            if left > right:

                return

            if left == right:

                self.tree[node] = arr[left]

            else:

                mid = (left + right) // 2

                Sum(arr, 2 * node + 1, left, mid)

                Sum(arr, 2 * node + 2, mid + 1, right)

                self.tree[node] = self.tree[2 * node + 1] + self.tree[2 * node + 2]

  

        Sum(arr, 0, self.left, self.right)

  

    def sum_update(self, index, value):

  

        def update(node, left, right, index, new_val):

            if left > right:

                return

            if left == right:

                self.tree[node] = new_val

            else:

                mid = (left + right) // 2

                if index <= mid:

                    update(2 * node + 1, left, mid, index, new_val)

                else:

                    update(2 * node + 2, mid + 1, right, index, new_val)

                self.tree[node] = self.tree[2 * node + 1] + self.tree[2 * node + 2]

        update(0, self.left, self.right, index, value)

  

    def sum_query(self, left_q, right_q):

  

        def query(node, left, right, left_q, right_q):

            if left > right or left > right_q or left_q > right:

                return 0

            if left >= left_q and right_q >= right:

                return self.tree[node]

            mid = (left + right) // 2

            return query(2 * node + 1, left, mid, left_q, right_q) + query(2 * node + 2, mid + 1, right, left_q, right_q)

        return query(0, self.left, self.right, left_q, right_q)

    def fn_build(self, arr, fn):

        self.fn = fn

        def compare(arr, node, left, right):

            if left > right:

                return

            if left == right:

                self.tree[node] = arr[left]

            else:

                mid = (left + right) // 2

                compare(arr, 2 * node + 1, left, mid)

                compare(arr, 2 * node + 2, mid + 1, right)

                self.tree[node] = fn(self.tree[2 * node + 1], self.tree[2 * node + 2])

  

        compare(arr, 0, self.left, self.right)

  

    def fn_update(self, index, value):

  

        def update(node, left, right, index, new_val):

            if left > right:

                return

            if left == right:

                self.tree[node] = new_val

            else:

                mid = (left + right) // 2

                if index <= mid:

                    update(2 * node + 1, left, mid, index, new_val)

                else:

                    update(2 * node + 2, mid + 1, right, index, new_val)

                self.tree[node] = self.fn(self.tree[2 * node + 1], self.tree[2 * node + 2])

        update(0, self.left, self.right, index, value)

  

    def fn_query(self, left_q, right_q):

  

        def query(node, left, right, left_q, right_q):

            if left > right or left > right_q or left_q > right:

                if self.fn == max:

                    return float('-inf')

                if self.fn == min:

                    return float('inf')

                if self.fn == gcd:

                    return 0

                if self.fn == lcm:

                    return 1

            if left >= left_q and right_q >= right:

                return self.tree[node]

            mid = (left + right) // 2

            return self.fn(query(2 * node + 1, left, mid, left_q, right_q), query(2 * node + 2, mid + 1, right, left_q, right_q))

        return query(0, self.left, self.right, left_q, right_q)
```
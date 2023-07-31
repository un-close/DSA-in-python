# To rotate anti-clockwise
```python
    def rotate_matrix_anticlockwise(matrix):

        n = len(matrix)

        m = len(matrix[0])

        rotated_matrix = [['#'] * n for _ in range(m)]

        for i in range(m):

            for j in range(n):

                rotated_matrix[i][j] = matrix[j][m - i - 1]

        return rotated_matrix
```

# To rotate clockwise:
```python
def rotate_matrix(matrix):
	return [list(row[::-1]) for row in zip(*matrix)]
```
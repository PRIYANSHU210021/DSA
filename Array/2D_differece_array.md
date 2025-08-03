
#  2D Difference Array — Efficient Submatrix Updates

##  Problem Statement

You are given:

* A 2D integer matrix `mat` of size `n × m`.
* A list of `q` operations `opr[][]`.

Each operation is represented as:

```
[v, r1, c1, r2, c2]
```

Where:

* `v`: Value to add.
* `(r1, c1)`: Top-left coordinate of submatrix.
* `(r2, c2)`: Bottom-right coordinate of submatrix (inclusive).

###  Task:
Apply all the operations efficiently and return the final matrix.

---

##  Naive Approach (Inefficient)

Loop through every cell from `(r1, c1)` to `(r2, c2)` and add `v`.

 Time Complexity: `O(q × n × m)` → Too slow for large inputs.

---

## ✅Efficient Approach: 2D Difference Array

Use a **2D difference matrix** to apply all range updates in constant time per operation.

###  Key Idea:

Instead of updating all elements in each submatrix directly, use inclusion-exclusion:

```cpp
diff[r1][c1] += v;
diff[r1][c2+1] -= v;
diff[r2+1][c1] -= v;
diff[r2+1][c2+1] += v;
```

Then compute prefix sums:

* First row-wise
* Then column-wise

This ensures each cell receives the correct cumulative effect of all operations.

---

##  Step-by-Step Algorithm

1. **Initialize** a 2D difference matrix `diff` of same size as `mat`.
2. **Apply** each operation using the 2D difference array technique.
3. **Compute** prefix sums:

   * Row-wise
   * Then column-wise
4. **Update** the original matrix: `mat[i][j] += diff[i][j]`
5. **Return** the updated matrix.

---

##  Time Complexity

* Applying operations: `O(q)`
* Prefix sums: `O(n × m)`
* Final update: `O(n × m)`

 Total: `O(q + n × m)` → **Efficient!**

---

##  C++ Implementation

```cpp
class Solution {
  public:
    vector<vector<int>> applyDiff2D(vector<vector<int>>& mat,
                                    vector<vector<int>>& opr) {
        int n = mat.size();
        int m = mat[0].size();
        vector<vector<int>> diff(n, vector<int>(m, 0));

        // Step 1: Apply all operations to the diff matrix
        for (const auto& op : opr) {
            int v = op[0];
            int r1 = op[1], c1 = op[2];
            int r2 = op[3], c2 = op[4];

            diff[r1][c1] += v;
            if (c2 + 1 < m) diff[r1][c2 + 1] -= v;
            if (r2 + 1 < n) diff[r2 + 1][c1] -= v;
            if (r2 + 1 < n && c2 + 1 < m) diff[r2 + 1][c2 + 1] += v;
        }

        // Step 2: Row-wise prefix sum
        for (int i = 0; i < n; i++) {
            for (int j = 1; j < m; j++) {
                diff[i][j] += diff[i][j - 1];
            }
        }

        // Step 3: Column-wise prefix sum
        for (int j = 0; j < m; j++) {
            for (int i = 1; i < n; i++) {
                diff[i][j] += diff[i - 1][j];
            }
        }

        // Step 4: Apply the diff matrix to the original matrix
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                mat[i][j] += diff[i][j];
            }
        }

        return mat;
    }
};
```

---

##  Example

### Input

```text
mat = [
  [1, 2],
  [3, 4]
]

opr = [
  [10, 0, 0, 1, 1],  // Add 10 to all elements from (0,0) to (1,1)
  [-5, 0, 1, 1, 1]   // Subtract 5 from column 1
]
```

### Output

```text
[
  [11, 7],
  [13, 9]
]
```

---

## 📎 References

* [Best Video Explanation](https://www.youtube.com/watch?v=uaWvpSC1Ye0)


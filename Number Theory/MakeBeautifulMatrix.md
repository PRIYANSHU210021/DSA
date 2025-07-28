```cpp
class Solution {
  public:
    int balanceSums(vector<vector<int>>& mat) {
        // code here 
        int n = mat.size();
        int maxi = 0; 
        for(int i=0; i<n; i++){
            int temp = 0;
            for(int j =0; j<n; j++)
            temp += mat[i][j];
            maxi = max(maxi, temp);
        }
        for(int i=0; i<n; i++){
            int temp = 0;
            for(int j =0; j<n; j++)
            temp += mat[j][i];
            maxi = max(maxi, temp);
        }
        
        int ans = 0;
        for(int i=0; i<n; i++){
                int temp = 0;
            for(int j=0; j<n; j++){
                temp += mat[i][j];
            }
            ans  += maxi - temp;
        }
        
        return ans;
    }
};
```


Sure! Here's the **core logic** behind your solution:

---

### 💡 **Core Logic:**

1. **Goal:**
   Make all **rows and columns** have the **same sum** using only **increment operations**.

2. **Key Insight:**
   Since you're only allowed to **increase** values, the only possible target for all row/column sums is the **maximum** row or column sum already present in the matrix.

3. **Why this works:**

   * Each increment in a cell affects both the **row and column** it belongs to.
   * So if you make **every row sum equal to the max**, the **column sums will also become equal** to that same max.

4. **What you do:**

   * Find the **maximum** among all row and column sums — this becomes your **target sum**.
   * For each row, calculate how much it **falls short** from the target.
   * Add up all the shortages → that’s the **minimum number of additions** required.

---


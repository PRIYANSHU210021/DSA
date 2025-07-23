```cpp
class Solution {
  public:
    int subarraySum(vector<int>& arr) {
        int n = arr.size();
        long long sum = 0;
        for(int i=0; i<n; i++){
            sum += (i*(n-i) + (n-i))*arr[i];
        }
        return sum;
    }
};  
```



---

### 🔍 Function: `subarraySum(vector<int>& arr)`

### 🧠 Approach Explained Step-by-Step:

* **Goal:** Calculate the **sum of all subarrays** of the array in **O(n)** time.

* **Looping over each element `arr[i]`:**

  * You're calculating its **contribution** to the sum of all subarrays.

* **Observation:**

  * For element at index `i`, it will be part of multiple subarrays.
  * It appears in:

    * **`(i + 1)`** possible starting points (from index 0 to `i`),
    * **`(n - i)`** possible ending points (from index `i` to `n - 1`),
    * So, total number of subarrays including `arr[i]` = `(i + 1) * (n - i)`

* **Your Formula:**

  ```cpp
  sum += (i * (n - i) + (n - i)) * arr[i];
  ```

  * This simplifies to:
    $(i + 1) * (n - i) * arr[i]$
  * Which is **correct**, but just written in a slightly expanded form:

    * `i * (n - i)` gives `(i * (n - i))`
    * `(n - i)` added again makes it `i * (n - i) + (n - i) = (i + 1) * (n - i)`

* **Accumulating total contribution:**

  * Each element's contribution is multiplied and added to the total `sum`.

* **Return value:**

  * You return `sum` as the final answer.

---

### ✅ Final Verdict:

* Your approach is **correct**, optimized to **O(n)**, and uses the **contribution technique**.
* Just a small suggestion:

  * You could directly use `(i + 1) * (n - i)` instead of expanding it for clarity.

---

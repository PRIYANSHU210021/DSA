```cpp
class Solution {
  public:
    int cntSubarrays(vector<int> &arr, int k) {
        int cnt = 0;
        int n = arr.size();
        int sum = 0;
        unordered_map<int,int>mp;
        for(int i=0; i<n; i++){
            sum += arr[i];
            if(sum==k) cnt++;
            if(mp.find(sum-k)!=mp.end()) cnt+= mp[sum-k];
            mp[sum]++;
        }
        return cnt;
    }
};
```
> **Count the number of subarrays with sum equal to `k`**.

---

## 🧠 Logic Explanation:

### ✅ Idea: **Prefix Sum + Hash Map**

You’re keeping track of the **running sum** (`prefix sum`) as you iterate through the array.

### 🔹 Step-by-Step Logic:

1. **Prefix Sum**:

   * At every index, you calculate the total sum from the start up to that index (`sum += arr[i]`).

2. **Direct Match**:

   * If `sum == k`, that means the **subarray from index 0 to i** has sum `k`. So you increment the count.

3. **Subarray Ending at i**:

   * If there’s any **previous prefix sum** equal to `sum - k`, then the subarray from the **next index after that prefix** up to current index `i` has sum `k`.
   * You find how many such previous `sum - k` values exist using a **hash map**, and add that count to your result.

4. **Update the Map**:

   * After checking, you record the current prefix sum `sum` in the map, increasing its frequency.

---

### 📌 Example (Dry Run):

For `arr = [1,2,3], k = 3`
Prefix Sums → `[1, 3, 6]`

* At index 1 (prefix sum = 3), `sum == k` → `cnt++`.
* At index 2, `sum = 6`, `sum - k = 3` → You’ve seen `3` before (from index 1), so subarray `[3]` has sum `k` → `cnt++`.

Final `cnt = 2` → `[1,2]` and `[3]`.

---

## 🔄 What You’ve Done:

* ✅ Used **prefix sum** to reduce redundant subarray sum calculations.
* ✅ Used a **hash map** to count all valid previous subarrays quickly.
* ✅ Achieved **O(n)** time complexity.

---

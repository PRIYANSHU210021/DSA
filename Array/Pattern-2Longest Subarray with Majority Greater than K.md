### *Given an array arr[ ] and an integer k, the task is to find the length of longest subarray in which the count of elements greater than k is more than the count of elements less than or equal to k.* ###

```cpp
class Solution {
  public:
    int longestSubarray(vector<int> &arr, int k) {
        // Code here
        int n = arr.size();
        int sum = 0;
        int maxi = 0;
        unordered_map<int,int>mp;
        for(int i=0; i<n; i++)        {
            if(arr[i] > k )
            sum += 1;
            else 
            sum--;
            if(sum > 0) maxi = max(i+1,maxi);
            if(mp.find(sum - 1)!=mp.end()){
                maxi = max(maxi , i - mp[sum-1]);
            }
            if(mp.find(sum)==mp.end())
            mp[sum] = i;    
        }
        return maxi;
    }
};
```

You're using a **clever prefix sum approach with a hashmap** to solve a common problem. Here's a breakdown and explanation of what this C++ code does, plus where and how it could apply.

---

### ✅ **Problem Being Solved:**

You are trying to find the **length of the longest subarray** where the number of elements **greater than `k` is more than the number of elements less than or equal to `k`**.

---

### 🔍 **Code Explanation:**

```cpp
int sum = 0; // keeps track of the running score: +1 for >k, -1 for <=k
int maxi = 0; // stores the max length of such a subarray
unordered_map<int,int> mp; // to store the first index where a particular sum occurred
```

#### Step-by-step logic:

1. **Iterate** through the array.
2. If `arr[i] > k`, treat it as +1.
   Else, treat it as -1.
3. Now:

   * If `sum > 0`, it means from index 0 to `i`, the number of elements > k is more → update `maxi`.
   * If `sum - 1` has occurred before, it means between that index and `i`, there's a segment where count of `>k` elements is more → calculate the length.
   * Store the first index of each `sum` value.

---

### 🧠 Example:

For `arr = [1, 3, 5, 2, 6]` and `k = 3`
`> k` → 5, 6 → treat as `+1`
`<= k` → 1, 3, 2 → treat as `-1`

Converted to: `[-1, -1, +1, -1, +1]`

The goal is to find the longest subarray where sum of this is **> 0**.

---

### 🔄 How It Works:

* It uses **prefix sum** like approach with hashmap to handle subarrays **efficiently in O(n)** time.
* Very similar in idea to problems like:

  * Longest subarray with equal number of 0s and 1s
  * Subarray sum equals k





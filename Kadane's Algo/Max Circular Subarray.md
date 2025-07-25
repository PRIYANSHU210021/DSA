```cpp
class Solution {
  public:
    int maxSS(vector<int>&arr){
        int n = arr.size();
        int maxi = INT_MIN;
        int sum = 0;
        for(int i=0; i<n; i++){
            sum = max(sum+arr[i],arr[i]);
            maxi = max(maxi, sum);
        }
       return maxi;  
    }
    int minSS(vector<int>&arr){
        int n = arr.size();
        int mini = INT_MAX;
        int sum = 0;
        for(int i=0; i<n; i++){
            sum = min(sum+arr[i],arr[i]);
            mini = min(mini, sum);
        }
       return mini;  
    }
    int maxCircularSum(vector<int> &arr) {
       int sum = 0;
       for(auto x:arr)
       sum += x;
       int maxi = maxSS(arr);
       int mini = minSS(arr);
       int maxCirSum = sum - mini;
       return (maxi > 0) ? max(maxi, maxCirSum) : maxi;
    }
};
```

---

## 🧠 **Thought Process:**

### 🎯 Problem:

Find the **maximum sum of a subarray**, where the subarray can be:

1. **Normal (non-circular)** — standard subarray like `[4, -1, 2, 1]`
2. **Circular** — can "wrap around" the array like `[3, -2, 5, -1, 2] → subarray: [2, 3, -2, 5]`

---

## 🔍 Insight:

The answer can be in **two possible ways**:

### ✅ **Case 1: Normal Kadane’s (non-circular)**

Just use **Kadane’s algorithm** to find the **maximum subarray sum**.

---

### ✅ **Case 2: Circular Subarray**

If the **maximum sum subarray is circular**, it means:

* You’re **excluding the minimum subarray** from the total array
* So, circular max sum = `totalSum - minSubarraySum`

> (Because removing the "worst" part gives the "best" wrap-around)

---

### ❗ Edge Case:

If **all elements are negative**, then:

* `totalSum - minSubarray` will become 0 or misleading
* So, we just return **normal Kadane’s** result (`maxi`)

---

## ✅ Final Formula:

```cpp
if (maxi > 0)
    return max(maxi, totalSum - mini);
else
    return maxi;
```

---

## 🧪 Example:

`arr = [5, -2, 3, 4]`

* `maxSS` (Kadane) = 10 → subarray: `[5, -2, 3, 4]`
* `minSS` = -2 → subarray: `[-2]`
* `totalSum = 10`
* `circularSum = 10 - (-2) = 12`

So final answer = `max(10, 12) = 12`

✔️ Wrap-around subarray = `[3, 4, 5]` (wrapped from end to start)

---

Would you like a visual diagram of how circular subarray works?

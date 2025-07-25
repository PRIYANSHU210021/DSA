**Kadane's Algorithm** is used to find the **maximum sum of a contiguous subarray** in a 1D array of integers (which may include both positive and negative numbers).

---

### 🧠 **Simple Concept (Think Like a Human):**

Imagine you're walking through a list of numbers and you're trying to **collect the maximum "gain"** along the way.
But if your current sum becomes **too negative**, it's better to **drop it and start fresh** from the next number.

---

### ✅ **Kadane's Algorithm Steps (Simple Language):**

1. **Start with 0 sum** and a very **small number for max sum** (like `-∞`).
2. For each number in the array:

   * Add it to your current sum.
   * If the current sum is **greater than max sum**, update the max sum.
   * If current sum becomes **negative**, reset it to 0 (start fresh).

---

### 🔍 Example:

Array: `[-2, 1, -3, 4, -1, 2, 1, -5, 4]`

Walkthrough:

| Index | Value | Current Sum | Max Sum |
| ----- | ----- | ----------- | ------- |
| 0     | -2    | 0 (reset)   | -2      |
| 1     | 1     | 1           | 1       |
| 2     | -3    | -2 (reset)  | 1       |
| 3     | 4     | 4           | 4       |
| 4     | -1    | 3           | 4       |
| 5     | 2     | 5           | 5       |
| 6     | 1     | 6           | 6       |
| 7     | -5    | 1           | 6       |
| 8     | 4     | 5           | 6       |

👉 **Max sum = 6**, from subarray `[4, -1, 2, 1]`

---

### 🧮 Code (C++ Style):

```cpp
int maxSubArray(vector<int>& nums) {
    int maxSum = INT_MIN;
    int currSum = 0;
    for(int num : nums) {
        currSum += num;
        maxSum = max(maxSum, currSum);
        if(currSum < 0) currSum = 0;
    }
    return maxSum;
}
```

---

### 💡 Kadane’s Magic:

* Works in **O(n)** time.
* Best for finding the **maximum subarray sum**.
* Reset the current sum when it hurts your total.

Want a visualization or dry-run on your custom array?


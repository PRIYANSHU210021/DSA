### *You are given an array of strings arr[], where each arr[i] consists of lowercase english alphabets. You need to find the number of balanced strings in arr[] which can be formed by concatinating one or more contiguous strings of arr[] , A balanced string contains the equal number of vowels and consonants. * ###

```cpp
class Solution {
  public:
    int countBalanced(vector<string>& arr) {
        // code here
        vector<int>v;
        for(auto x:arr){
            int b = 0;
            for(auto ch : x){
                if(ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' ||
                ch == 'u'){
                    b++;
                }
                else b--;
            }
            v.push_back(b);
        }
        unordered_map<int,int>mp;
        int cnt=0;
        int sum = 0;
        for(int i=0; i<v.size(); i++){
            sum += v[i];  
            if(sum == 0) cnt++;
            if(mp.find(sum)!=mp.end()){
                cnt += mp[sum];
            }
            mp[sum]++;
        }
        return cnt;
    }
};
```




### Problem:

You're given an array of strings. You need to count how many **subarrays** (contiguous subsets) of strings have an equal number of vowels and consonants combined.

#### Approach:

The solution uses a **prefix sum** technique with a hashmap to count how many subarrays are "balanced" (vowels == consonants).

### Code Breakdown:

```cpp
class Solution {
  public:
    int countBalanced(vector<string>& arr) {
        vector<int> v;  // stores the net vowel-consonant difference for each string
        for(auto x : arr) {
            int b = 0;  // Tracks the net balance of vowels and consonants in each string
            for(auto ch : x) {
                if(ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u') {
                    b++;  // Increment for vowels
                } else {
                    b--;  // Decrement for consonants
                }
            }
            v.push_back(b);  // Store the balance for this string
        }

        unordered_map<int, int> mp;  // Stores the frequency of prefix sums
        int cnt = 0, sum = 0;  // `cnt` for counting balanced subarrays, `sum` for the running prefix sum
        for(int i = 0; i < v.size(); i++) {
            sum += v[i];  // Update the running prefix sum
            if(sum == 0) {
                cnt++;  // If the sum is 0, the subarray from 0 to i is balanced
            }
            if(mp.find(sum) != mp.end()) {
                cnt += mp[sum];  // Add the number of previous occurrences of this sum
            }
            mp[sum]++;  // Increment the frequency of the current prefix sum
        }
        return cnt;
    }
};
```

### **Dry Run Example:**

Let’s dry-run the code with the following input:

```cpp
arr = ["ae", "bd", "u", "z"]
```

Here’s the step-by-step breakdown:

---

#### **Step 1: Convert each string into a vowel-consonant balance**:

We go through each string and calculate the **balance of vowels and consonants** for each string:

1. **String "ae"**:

   * Vowels = 'a', 'e' → 2 vowels
   * Consonants = 0 → balance = +2
   * `v.push_back(2)`

2. **String "bd"**:

   * Vowels = 0
   * Consonants = 'b', 'd' → 2 consonants
   * balance = -2
   * `v.push_back(-2)`

3. **String "u"**:

   * Vowels = 'u' → 1 vowel
   * Consonants = 0 → balance = +1
   * `v.push_back(1)`

4. **String "z"**:

   * Vowels = 0
   * Consonants = 'z' → 1 consonant
   * balance = -1
   * `v.push_back(-1)`

After this, the vector `v` becomes:

```
v = [2, -2, 1, -1]
```

This vector represents the balance of vowels and consonants for each string in the input array.

---

#### **Step 2: Prefix sum calculation with hashmap**:

Now, we calculate the **prefix sum** (the cumulative sum of values in `v`) and use a hashmap (`mp`) to track how many times a certain prefix sum has occurred.

1. **Initialization**:
   `cnt = 0` (to count balanced subarrays),
   `sum = 0` (running prefix sum),
   `mp = {}` (hashmap to store the frequency of prefix sums).

2. **First Iteration (`i = 0`)**:

   * Current value `v[0] = 2`.
   * Update `sum`:
     `sum = sum + 2 = 0 + 2 = 2`.
   * Since `sum == 0` is **false**, no increment in `cnt`.
   * No previous `sum == 2` in the hashmap, so add it:
     `mp[2] = 1`.

   **Current state**:

   * `sum = 2`, `cnt = 0`, `mp = {2: 1}`.

3. **Second Iteration (`i = 1`)**:

   * Current value `v[1] = -2`.

   * Update `sum`:
     `sum = sum + (-2) = 2 + (-2) = 0`.

   * Since `sum == 0` is **true**, increment `cnt` (because from index `0` to `1`, the subarray is balanced).
     `cnt = 1`.

   * `sum = 0` has occurred before (it’s the initial state), so increment `cnt` by the frequency of `sum == 0` in the hashmap:
     `cnt += mp[0]`, but `mp[0]` is not yet in the hashmap, so we increment `cnt = 1`.

   * Add `sum = 0` to the hashmap:
     `mp[0] = 1`.

   **Current state**:

   * `sum = 0`, `cnt = 1`, `mp = {2: 1, 0: 1}`.

4. **Third Iteration (`i = 2`)**:

   * Current value `v[2] = 1`.
   * Update `sum`:
     `sum = sum + 1 = 0 + 1 = 1`.
   * Since `sum == 0` is **false**, no increment in `cnt`.
   * No previous `sum == 1` in the hashmap, so add it:
     `mp[1] = 1`.

   **Current state**:

   * `sum = 1`, `cnt = 1`, `mp = {2: 1, 0: 1, 1: 1}`.

5. **Fourth Iteration (`i = 3`)**:

   * Current value `v[3] = -1`.

   * Update `sum`:
     `sum = sum + (-1) = 1 + (-1) = 0`.

   * Since `sum == 0` is **true**, increment `cnt` (because from index `0` to `3`, the subarray is balanced).
     `cnt = 2`.

   * `sum == 0` has occurred before (in the second iteration), so increment `cnt` by the frequency of `sum == 0` in the hashmap:
     `cnt += mp[0]`, so `cnt = 2 + 1 = 3`.

   * Add `sum = 0` to the hashmap:
     `mp[0] = 2`.

   **Final state**:

   * `sum = 0`, `cnt = 3`, `mp = {2: 1, 0: 2, 1: 1}`.

---

#### **Step 3: Return the result**:

After iterating through the array, the final value of `cnt` is `3`, which represents the number of balanced subarrays. So, the function returns `cnt = 3`.

---

### **Summary of Balanced Subarrays:**

* \["ae", "bd"] (index 0 to 1)
* \["u", "z"] (index 2 to 3)
* \["ae", "bd", "u", "z"] (full array)

So, the answer is `3`.

---

### Conclusion:

This solution efficiently finds the number of **balanced subarrays** by using a combination of **prefix sums** and **hash maps** to track the frequency of prefix sums. The time complexity of the solution is **O(n)**, where `n` is the number of strings in the input array.
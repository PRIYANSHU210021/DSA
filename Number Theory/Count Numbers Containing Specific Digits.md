Ques:

Count Numbers Containing Specific Digits
Difficulty: MediumAccuracy: 70.94%Submissions: 2K+Points: 4Average Time: 25m
You are given an integer n representing the number of digits in a number, and an array arr[] containing digits from 0 to 9. Your have to count how many n-digit positive integers can be formed such that at least one digit from the array arr[] appears in the number.

Examples:

Input: n = 1, arr[] = [1, 2, 3]
Output: 3
Explanation: Only the single-digit numbers [1, 2, 3] satisfy the condition.
Input: n = 2, arr[] = [3, 5]
Output: 34
Explanation: There are a total of 34  two digit numbers which contain atleast  one out of  [3, 5].
Constraints:
  1 ≤ n ≤ 9
  1 ≤ arr.size() ≤ 10
  0 ≤ arr[i] ≤ 9



```cpp
class Solution {
  public:
    int countValid(int m, vector<int>& arr) {
        int s = arr.size();
        int flag = 0;
        set<int>st;
        for(int i=0; i<s; i++){
            st.insert(arr[i]);
            if(arr[i]==0)
            flag =1;
        }
        int ss = st.size();
        int temp1=9-ss;
        if(flag == 1)
            temp1 = 10-ss;
        int n = m;
        n--;
        while(n--)
            temp1 = temp1*(10-ss);
        int total = 9 * pow(10,m-1);
        return total - temp1;
    }
};
```


***WHAT i learn first chatgpt***

You're asking:

> **If I build all numbers with 3 digits (i.e., numbers from 000 to 999), how many of them have the digit `8` appear at least once?**

---
### **What I ask first " if i built a number of digit 3, so how many no. formed in which at least 1 time 8 appear "** ###

### ✅ **Approach: Complement Method (Total - Not having 8)**

Let’s use the **complement method**:

* **Total 3-digit numbers (with digits 0–9):** $10 \times 10 \times 10 = 1000$ (from 000 to 999)
* **Count of numbers with no 8 at all**:

  * Each digit has 9 choices (0–9 except 8) → so:
  * $9 \times 9 \times 9 = 729$

✅ So, the number of 3-digit numbers **with at least one '8'** =

$$
1000 - 729 = \boxed{271}
$$

---

### 🎯 Final Answer: **271** numbers contain at least one `8`

Let me know if you want to apply this logic to numbers with `n` digits.




---
---------------------------------------
---

### My Next Question follow up question is that is i said ki aik or number hai 8 ke sath , 3 ab dono ka sath me btao agar same no. ho to 1 time considered krna

Great follow-up! Let's break it down properly.

---

### ❓Question:

> In **3-digit numbers (000 to 999)**, how many numbers contain **at least one `8` *or* one `3`** (or both)?
> If a number has **both `8` and `3`**, **count it only once**.

---

### ✅ Total possible 3-digit numbers (with leading 0 allowed):

$$
10 \times 10 \times 10 = 1000
$$

We'll use the **inclusion-exclusion principle**.

---

### Step 1: Count numbers **with no 8 and no 3**

Digits allowed = {0, 1, 2, 4, 5, 6, 7, 9} → total 8 choices per digit (excluding 3 and 8)

$$
\text{No 8 and no 3} = 8 \times 8 \times 8 = 512
$$

---

### Step 2: Now use complement

$$
\text{At least one 8 or one 3} = \text{Total} - \text{No 3 and no 8} = 1000 - 512 = \boxed{488}
$$

---

### ✅ Final Answer:

$$
\boxed{488} \text{ numbers have at least one 8 or one 3 (or both), counted only once.}
$$

Let me know if you want this for numbers without leading zeros (like 100–999) too!

---
---
---

### Next if i replace 3 digit with 2 then
Great! Let's now solve for **2-digit numbers** (from `00` to `99`) and find how many numbers have **at least one `8` or one `3`**, counted only once even if both appear.

---

### ✅ Total 2-digit numbers (including `00` to `99`):

$$
10 \times 10 = 100
$$

---

### Step 1: Count numbers with **no 3 and no 8**

Allowed digits = {0, 1, 2, 4, 5, 6, 7, 9} → 8 choices per digit

$$
8 \times 8 = 64 \text{ numbers without any 3 or 8}
$$

---

### Step 2: Complement to get at least one 3 or 8

$$
\text{At least one 3 or 8} = 100 - 64 = \boxed{36}
$$

---

### ✅ Final Answer:

$$
\boxed{36} \text{ two-digit numbers (00 to 99) contain at least one 3 or 8 (or both).}
$$

Let me know if you want this without leading zeros (i.e., only from 10 to 99)!

---
---
---


### Next bro but ans is 34

You're **absolutely right to double-check** — and yes, let's clear it up now by answering precisely:

> **How many 2-digit numbers (from 10 to 99) have at least one 8 or one 3? Count each number once, even if it has both.**

---

### ✅ Step 1: Total 2-digit numbers

From **10 to 99**, the total count is:

$$
99 - 10 + 1 = 90
$$

---

### ✅ Step 2: Count how many 2-digit numbers have **no 8 and no 3**

We eliminate all numbers that contain either **3** or **8** in **either digit**.

* Loop over all 2-digit numbers from 10 to 99.
* Keep only those numbers that **do not** contain `3` or `8`.

Let’s do this manually or logically:

**Allowed digits (excluding 3 and 8):**

* Valid digits: `{0, 1, 2, 4, 5, 6, 7, 9}` → 8 valid digits

So now:

* First digit (tens place): from 1 to 9 → excluding 3 and 8 → `{1, 2, 4, 5, 6, 7, 9}` → 7 options
* Second digit (ones place): 0 to 9 → excluding 3 and 8 → 8 options

$$
\text{No 3 or 8} = 7 \times 8 = 56
$$

---

### ✅ Step 3: Subtract from total 2-digit numbers

$$
\text{At least one 3 or 8} = 90 - 56 = \boxed{34}
$$

---

### ✅ Final Answer:

There are **34 two-digit numbers** (from 10 to 99) that have **at least one occurrence of 3 or 8**.

You were correct — **well spotted!** ✅

---
---
---

### Next and for 3 digit


Great! Let’s now calculate:

> **How many 3-digit numbers (from 100 to 999) contain at least one `3` or `8` (count each number only once, even if both are present)?**

---

### ✅ Step 1: Total 3-digit numbers

$$
\text{From 100 to 999} \Rightarrow 999 - 100 + 1 = \boxed{900}
$$

---

### ✅ Step 2: Count how many 3-digit numbers **do NOT contain `3` or `8`**

We'll subtract those from 900.

---

#### 🔸 Allowed digits (excluding `3` and `8`):

`{0, 1, 2, 4, 5, 6, 7, 9}` → **8 valid digits**

* **Hundreds digit (1–9):** cannot be `3` or `8`, and not `0`
  → Valid options: `{1, 2, 4, 5, 6, 7, 9}` → **7 options**

* **Tens digit (0–9):** excluding `3`, `8` → **8 options**

* **Units digit (0–9):** excluding `3`, `8` → **8 options**

So total 3-digit numbers **without** 3 or 8:

$$
7 \times 8 \times 8 = \boxed{448}
$$

---

### ✅ Step 3: Subtract from total

$$
900 - 448 = \boxed{452}
$$

---

### ✅ Final Answer:

There are **452** three-digit numbers (from 100 to 999) that contain **at least one `3` or `8`**.



---
---
---





To calculate how many **n-digit numbers** exist, use this formula:

---

### ✅ **Formula for total `n`-digit numbers**:

$$
\text{Total} = 9 \times 10^{n - 1}
$$

---

### ✅ **Why?**

* **First digit** (most significant digit) must be **1–9** → 9 options
* **Remaining (n-1) digits** can be **0–9** → 10 options each

---

### ✅ Examples:

* **1-digit numbers**: $1$ to $9$ → $9$
* **2-digit numbers**: $10$ to $99$ → $9 \times 10 = \boxed{90}$
* **3-digit numbers**: $100$ to $999$ → $9 \times 100 = \boxed{900}$
* **4-digit numbers**: $1000$ to $9999$ → $9 \times 1000 = \boxed{9000}$

---
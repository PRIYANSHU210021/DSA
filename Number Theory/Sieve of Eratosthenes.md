```cpp
class Solution {
  public:
    vector<int> sieve(int n) {
        vector<int>prime(n+1,1);
        
        for(int i=2; i*i <= n; i++){
            if(prime[i] == 1){
                for(int j = i*i; j<=n; j=j+i){
                    prime[j]=0;
                }
            }
        }
        
        vector<int>ans;
        for(int i=2; i<=n; i++){
            if(prime[i]==1){
                ans.push_back(i);
            }
        }
        return ans;
    }
};
```


---

# 🌟 Sieve of Eratosthenes – Explained Elegantly

The **Sieve of Eratosthenes** is one of the most efficient ways to find all **prime numbers** up to a given number `n`.

---

## 🔧 Function Signature

```cpp
vector<int> sieve(int n)
```

This function returns a list of all **prime numbers ≤ n**.

---

## 💡 What’s the Idea?

We begin by **assuming all numbers are prime**, and then we **eliminate** the non-primes (multiples of each number) in a smart way.

---

## 🧠 Step-by-Step Logic

### 1️⃣ Create a Boolean Prime Table

```cpp
vector<int> prime(n + 1, 1);
```

* We initialize a vector of size `n+1` with all entries as `1` (meaning "true").
* This marks every number from `0` to `n` as prime initially.

---

### 2️⃣ Eliminate Non-Primes Using Sieve Logic

```cpp
for (int i = 2; i * i <= n; i++) {
    if (prime[i] == 1) {
        for (int j = i * i; j <= n; j += i) {
            prime[j] = 0;
        }
    }
}
```

* We iterate from `i = 2` up to `√n`.
* If `i` is marked prime:

  * We mark all **multiples of `i`** as **not prime** starting from `i × i`.
  * Why from `i*i`? Because smaller multiples would have been handled by smaller primes earlier.

---

### 3️⃣ Collect All Remaining Primes

```cpp
vector<int> ans;
for (int i = 2; i <= n; i++) {
    if (prime[i] == 1) {
        ans.push_back(i);
    }
}
return ans;
```

* After marking, all numbers that are **still `1`** in the `prime[]` array are **prime numbers**.
* We gather them in the `ans` vector and return it.

---

## 📌 Example: `sieve(10)`

| Index  | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | 10  |
| ------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Prime? | ✅   | ✅   | ❌   | ✅   | ❌   | ✅   | ❌   | ❌   | ❌   |

✅ Final primes: `[2, 3, 5, 7]`

---

## 🕒 Time Complexity

* **Initialization:** `O(n)`
* **Sieve Loop:** `O(n log log n)` – very efficient
* **Collecting Primes:** `O(n)`

---

## ✅ Summary

| Feature         | Value                 |
| --------------- | --------------------- |
| Purpose         | List primes ≤ `n`     |
| Algorithm       | Sieve of Eratosthenes |
| Time Complexity | `O(n log log n)`      |
| Space Used      | `O(n)`                |

---

Let me know if you'd like the code visualized with animations, flowchart, or in another language like Python/Java!

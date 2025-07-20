Here's the **corrected and optimized C++ code** to count numbers ≤ `n` that have **exactly 9 divisors**:

---

### ✅ Final Code:

```cpp
class Solution {
  public:
    int countNumbers(int n) {
        int limit = sqrt(n) + 1;
        vector<int> primes(limit + 1, 1);

        // Sieve of Eratosthenes to find all prime numbers up to sqrt(n)
        for (int i = 2; i * i <= limit; i++) {
            if (primes[i]) {
                for (int j = i * i; j <= limit; j += i) {
                    primes[j] = 0;
                }
            }
        }

        vector<int> primeList;
        for (int i = 2; i <= limit; i++) {
            if (primes[i]) {
                primeList.push_back(i);
            }
        }

        int count = 0;

        // Case 1: p^8 (only 1 such prime p where p^8 ≤ n)
        for (int p : primeList) {
            long long num = 1;
            for (int i = 0; i < 8; i++) {
                num *= p;
                if (num > n) break;
            }
            if (num <= n) count++;
        }

        // Case 2: p^2 * q^2 (where p ≠ q are distinct primes)
        int size = primeList.size();
        for (int i = 0; i < size; i++) {
            for (int j = i + 1; j < size; j++) {
                long long val = 1LL * primeList[i] * primeList[i] * primeList[j] * primeList[j];
                if (val <= n) count++;
                else break;  // further j will increase val
            }
        }

        return count;
    }
};
```

---

### 🧠 Simple Explanation:

We're looking for numbers with **exactly 9 divisors**. The trick is to understand that:

> **Only two types of numbers have exactly 9 divisors:**
>
> 1. **p⁸** → A single prime raised to the power 8
>    (e.g., 2⁸ = 256 → divisors = 8 + 1 = 9)
>
> 2. **p² × q²** → Two different primes, each raised to power 2
>    (e.g., 2² × 3² = 36 → (2+1)(2+1) = 9 divisors)

---

### 🔍 Why These Two Forms Only?

* Total divisors = (a+1)(b+1)... for prime powers: `p^a * q^b * ...`
* We want product of exponents+1 = 9
* 9 = 9 → p⁸
* 9 = 3×3 → p² \* q²

---

### ✅ Steps Done:

1. **Sieve up to √n** to get all primes.
2. **Loop through primes** to:

   * Try `p^8` (just once per prime)
   * Try all valid combinations `p^2 * q^2` where `p ≠ q`
3. Count the values ≤ `n`.

---

Let me know if you want this in Python too, or a dry-run with a sample like `n = 200`.

```cpp
Power of k in factorial of n    
```

> **`k` ki maximum power find karni jo `n!` (n factorial) ko completely divide karti ho.**

---

## 🧩 Step-by-step Breakdown (Hinglish):

---

### 🔶 Step 1: **Sieve of Eratosthenes se Prime Numbers nikalna**

```cpp
int limit = k + 1;
vector<int> primes(limit, 1);
primes[0] = primes[1] = 0;
```

🔸 Hum `2` se lekar `k` tak ke sabhi **prime numbers** find kar rahe hain using sieve.

```cpp
for (int i = 2; i * i < limit; i++) {
    if (primes[i]) {
        for (int j = i * i; j < limit; j += i) {
            primes[j] = 0;
        }
    }
}
```

🔸 Agar koi number prime hai (`primes[i] == 1`), toh uske sabhi multiples ko mark kar dete hain as non-prime.

```cpp
for (int i = 2; i < limit; i++) {
    if (primes[i]) {
        primeList.push_back(i);
    }
}
```

🔸 Ab humne `primeList` bana liya — jisme 2 se k tak ke sab prime numbers hain.

---

### 🔶 Step 2: **k ka Prime Factorization**

```cpp
int temp = k;
```

🔸 Ab hum `k` ko todte hain uske prime factors mein. Jaise:
> Agar `k = 180` ho → `2^2 * 3^2 * 5^1`

```cpp
for (int i = 0; i < primeList.size() && temp > 1; i++) {
    int cnt = 0;
    while (temp % primeList[i] == 0) {
        cnt++;
        temp /= primeList[i];
    }
    if (cnt > 0) {
        cntPrimes.push_back(cnt);       // kitni baar aaya
        actualPrimes.push_back(primeList[i]); // kaunsa prime tha
    }
}
```

🧠 `cntPrimes` me store ho raha hai har prime ki power  
🧠 `actualPrimes` me store ho raha hai kaunse prime factors hain

---

### ⚠️ Special Case: **Bacha hua temp agar ek bada prime ho**

```cpp
if (temp > 1) {
    cntPrimes.push_back(1);
    actualPrimes.push_back(temp);
}
```

🔸 Agar koi prime factor `sqrt(k)` se bada hai (jaise `k = 77 → 7 * 11`, jisme `11 > sqrt(77)`),  
toh wo sieve se nahi milega, **isliye usse manually add kiya jaata hai**.

---

### 🔶 Step 3: **Har Prime ki Power Count karo in `n!`**

```cpp
for (int i = 0; i < actualPrimes.size(); i++) {
    int p = actualPrimes[i];
    int res = 0;
    long long power = p;
    while (n / power > 0) {
        res += n / power;
        power *= p;
    }
    fans.push_back(res);
}
```

📌 Yeh **Legendre’s Formula** use karta hai:  
**power of p in n! = n/p + n/p² + n/p³ + ...**

> Iska matlab: `n!` mein kisi prime `p` ki kitni power hai uska total count nikalna.

---

### 🔶 Step 4: **Final Answer = Minimum of all `fans[i] / cntPrimes[i]`**

```cpp
int maxAns = INT_MAX;
for (int i = 0; i < cntPrimes.size(); i++) {
    maxAns = min(maxAns, fans[i] / cntPrimes[i]);
}
```

🔸 For example:

| Prime Factor | Count in n! | Count in k | fans[i] / cntPrimes[i] |
|--------------|-------------|------------|--------------------------|
| 2            | 47          | 2          | 23                       |
| 3            | 22          | 2          | 11                       |
| 5            | 12          | 1          | 12                       |

🟢 Final answer = **min(23, 11, 12) = 11**

---

## ✅ Final Return:
```cpp
return maxAns;
```
➡️ `k^maxAns` divides `n!` completely but `k^(maxAns+1)` doesn't.

---

## 📦 Summary:
- Pehle `k` ko prime factors mein toda
- Fir `n!` mein har prime ki power count ki
- Har prime ke liye `fans[i] / cntPrimes[i]` liya
- Minimum value return ki

---

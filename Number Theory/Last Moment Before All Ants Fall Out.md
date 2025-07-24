```cpp
class Solution {
  public:
    int getLastMoment(int n, vector<int>& left, vector<int>& right) {
       int n1 = left.size();
       int n2 = right.size();
       int maxi1 = INT_MIN;
       int maxi2 = INT_MIN;
       for(int i=0; i<n1; i++){
           maxi1 = max(maxi1,left[i]);
       }
       for(int i=0; i<n2; i++){
           maxi2 = max(maxi2,n-right[i]);
       }
       
       return max(maxi1,maxi2);
    }
};
```

---

> ❓ **“When ant moves right or left, and it may collide, I’m ignoring collision.”**

✔️ **Correct.**
Because when two ants collide, they **pass through each other** (just swap identities). So collision **does not affect the timing or positions** — you can ignore it completely.

---

> ❓ **“I just think only what is the maximum time of ant who goes left and right only.”**

✔️ **Correct.**

* For **left-moving ants**, the one **farthest from 0** takes the longest to fall.
* For **right-moving ants**, the one **closest to 0** takes the longest to fall off at `n`.

---

> ❓ **“Last return maxi among both left maximum and right maximum.”**

✔️ **Exactly.**

* You're finding the **maximum time** it takes for **any ant** to fall off.
* So you return:

  ```cpp
  return max(max_time_from_left, max_time_from_right);
  ```

---

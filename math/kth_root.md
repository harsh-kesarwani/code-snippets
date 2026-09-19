# Integer k-th root

Largest integer `x` with `x^k <= n` (i.e. `floor(n^(1/k))`), via binary search on
the answer. (`n >= 0`, `k > 0`)

- Time: O(k log n)
- Space: O(1)

```cpp
long long kthRoot(long long n, int k) {
    long long low = 0, high = n, ans = 0;

    while (low <= high) {
        long long mid = low + (high - low) / 2;

        if (power(mid, k, n) <= n) {
            ans = mid;
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }
    return ans;
}
```

## Power (overflow-safe)

Computes `base^k`, returning `limit + 1` if it would exceed `limit` (checks
before multiplying, so the result never overflows).

- Time: O(k)
- Space: O(1)

```cpp
long long power(long long base, int k, long long limit) {
    if (base == 0) return 0;
    long long result = 1;
    for (int i = 0; i < k; i++) {
        if (result > limit / base)
            return limit + 1;
        result *= base;
    }
    return result;
}
```

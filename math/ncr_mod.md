# nCr (Modular)

Compute `nCr % mod` using modular inverse (Fermat's little theorem, `mod` prime).
Requires `modPow` (below).

- Time: O(r log mod)
- Space: O(1)

```cpp
long long nCr(int n, int r, int mod) {
    if (r < 0 || r > n) return 0;
    r = min(r, n - r);

    long long ans = 1;
    for (int i = 1; i <= r; i++) {
        ans = ans * (n - r + i) % mod;
        ans = ans * modPow(i, mod - 2, mod) % mod;
    }
    return ans;
}
```

## Modular Exponentiation

Fast `base^exp % mod` by binary exponentiation (squaring).

- Time: O(log exp)
- Space: O(1)

```cpp
long long modPow(long long base, long long exp, int mod) {
    long long res = 1;
    while (exp) {
        if (exp & 1) res = res * base % mod;
        base = base * base % mod;
        exp >>= 1;
    }
    return res;
}
```

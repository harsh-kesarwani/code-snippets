# SPF Array (Smallest Prime Factor)

- Time: O(n log log n)
- Space: O(n)

```cpp
vector<int> buildSPF(int n) {
    vector<int> spf(n + 1);
    for (int i = 0; i <= n; i++) spf[i] = i;

    for (int i = 2; i * i <= n; i++) {
        if (spf[i] != i) continue;          // not prime
        for (int j = i * i; j <= n; j += i) {
            if (spf[j] == j)
                spf[j] = i;
        }
    }
    return spf;
}
```

After building the SPF array, we can get prime factors of any number:

- Time: O(log n)
- Space: O(1)

```cpp
vector<int> getPrimeFactors(int x, const vector<int>& spf) {
    vector<int> factors;

    while (x > 1) {
        int p = spf[x];
        factors.push_back(p);

        while (x % p == 0)
            x /= p;
    }

    return factors;
}
```

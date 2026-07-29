# Sieve of Eratosthenes

Find all the prime numbers up to `n`.

- Time: O(n log log n)
- Space: O(n)

```cpp
// n from 0 to INT_MAX

vector<int> sieve(int n) {
    if (n < 2) return {};
    vector<bool> isPrime(n + 1, true);
    isPrime[0] = isPrime[1] = false;
    for (int i = 2; i <= n / i; i++) {
        if (!isPrime[i]) continue;
        for (int j = i * i; j <= n; j += i) {
            isPrime[j] = false;
        }
    }
    vector<int> primes;
    for (int i = 2; i <= n; i++) {
        if (isPrime[i]) primes.push_back(i);
    }
    return primes;
}
```

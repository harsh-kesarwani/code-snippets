# GCD - Euclidean Algorithm

Greatest common divisor of two integers using repeated remainders.

## Recursive

- Time: O(log(min(a, b)))
- Space: O(log(min(a, b)))

```cpp
int gcd(int a, int b) {
    if (b == 0)
        return a;
    return gcd(b, a % b);
}
```

## Iterative

- Time: O(log(min(a, b)))
- Space: O(1)

```cpp
int gcd(int a, int b) {
    while (b != 0) {
        int rem = a % b;
        a = b;
        b = rem;
    }
    return a;
}
```

The `gcd` function in the C++ standard library is based on the Euclidean algorithm.

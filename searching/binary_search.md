# Binary Search

Search a sorted array by halving the range each step. All variants below share
the same complexity.

- Time: O(log n)
- Space: O(1)

## 1. Exact Search

Find exact target value.

- Invariant: if target exists, it is always inside the range `[left, right]`.
- If `left > right`, search space is empty, loop stops.

```cpp
int binarySearch(vector<int>& v, int target) {
    int n = v.size(), left = 0, right = n - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (v[mid] == target)
            return mid;
        else if (v[mid] < target)
            left = mid + 1;
        else
            right = mid - 1;
    }

    return -1; // not found
}
```

## 2. Boundary Search

Find boundary: the smallest index `i` such that a given condition is true
("first-true" template).

- Condition must be monotonic -> result changes only in one direction, e.g. `FFFFTTTTTTT`.
- `right` should start from `n` (not `n - 1`), as the answer can be `n`.
- Invariant: the answer is always inside the range `[left, right]`.
- If `left == right`, range collapsed, this must be the answer.

```cpp
int firstTrue(vector<int>& v) {
    int n = v.size(), left = 0, right = n;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (/* condition(mid) */)
            right = mid;      // mid might be first true
        else
            left = mid + 1;   // first true is after mid
    }
    return left;
}
```

### 2a. Lower Bound

Condition: `v[mid] >= target`.

```cpp
int lowerBound(vector<int>& v, int target) {
    int n = v.size(), left = 0, right = n;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (v[mid] >= target)
            right = mid;
        else
            left = mid + 1;
    }
    return left;
}
```

### 2b. Upper Bound

Condition: `v[mid] > target`.

```cpp
int upperBound(vector<int>& v, int target) {
    int n = v.size(), left = 0, right = n;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (v[mid] > target)
            right = mid;
        else
            left = mid + 1;
    }
    return left;
}
```

### 2c. Alternate (closed-range `[low, high]`)

Another version for finding lower and upper bound using an inclusive range.

```cpp
int lowerBound(int low, int high, int target) {
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (v[mid] >= target)
            high = mid - 1;
        else
            low = mid + 1;
    }
    return low;
}
```

```cpp
int upperBound(int low, int high, int target) {
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (v[mid] > target)
            high = mid - 1;
        else
            low = mid + 1;
    }
    return low;
}
```

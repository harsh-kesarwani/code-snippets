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
- Returns the first true index, or `n` if none.

### Approach
- `right` should start from `n` (not `n - 1`), as the answer can be `n`.
- Invariant: the answer is always inside the closed range `[left, right]`.
- If `left == right`, range collapsed, this must be the answer.
- If `mid` is true, eliminate elements after `mid`, if false, eliminate elements upto `mid`.

```cpp
int firstTrue(vector<int>& v) {
    int n = v.size(), left = 0, right = n;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (/* v[mid] satisfies condition */)     // mid = T
            right = mid;                          // elements after mid eliminated
        else                                      // mid = F
            left = mid + 1;                       // elements upto mid eliminated
    }
    return left;
}
```

### Applications (Upper Bound / Lower Bound)

For a sorted array, replace the condition in generic template:

#### Lower Bound
Condition: `v[mid] >= target`

#### Upper Bound
Condition: `v[mid] > target`

---

### Alternative Approach

- `left <= right`, `right = n - 1`; search the inclusive range `[left, right]`.
- Invariant: indices before `left` are false; indices after `right` are true.
- Stop when `left > right`; `left` is the answer.
- True at `mid`: search earlier with `right = mid - 1`; false: `left = mid + 1`.

```cpp
int firstTrue(vector<int>& v) {
    int n = v.size(), left = 0, right = n - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (/* v[mid] satisfies condition */)
            right = mid - 1;
        else
            left = mid + 1;
    }
    return left;
}
```

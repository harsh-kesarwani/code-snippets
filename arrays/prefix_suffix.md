# Prefix / Suffix Arrays

```cpp
vector<int> pref(n + 1);

pref[0] = /* initial state */;
for (int i = 0; i < n; i++) {
    pref[i + 1] = update(pref[i], s[i]);
}


vector<int> suff(n + 1);

suff[n] = /* initial state */;
for (int i = n - 1; i >= 0; i--) {
    suff[i] = update(suff[i + 1], s[i]);
}
```

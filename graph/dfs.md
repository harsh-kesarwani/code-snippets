# DFS

- Time: O(V + E)
- Space: O(V)

### Recursive
default

```cpp
unordered_set<Node*> visited;

void dfs(Node* node) {
    if (!node) return;
    if (visited.count(node)) return;
    visited.insert(node);

    // process node

    for (auto x : node->neighbors) {
        dfs(x);
    }
}
```

### Iterative

TBA
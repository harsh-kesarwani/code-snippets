# BFS

- Time: O(V + E)
- Space: O(V)

```cpp
void bfs(Node* node) {
    if (!node) return;

    queue<Node*> q;
    unordered_set<Node*> visited;

    q.push(node);
    visited.insert(node);

    while (!q.empty()) {
        Node* curr = q.front();
        q.pop();

        // process node

        for (auto x : curr->neighbors) {
            if (!visited.count(x)) {
                visited.insert(x);
                q.push(x);
            }
        }
    }
}
```

# BFS (Binary Tree)

Notes:
- BFS is naturally iterative (level-order); uses a queue.

- Time: O(n)
- Space: O(w) -> O(n) (as w ≈ n/2)

## Level order

Algorithm:
- Push root to queue.
- While queue is not empty:
    - Dequeue node, process it.
    - Enqueue left and right children.

```cpp
void bfs(TreeNode* root) {
    if (!root) return;

    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        TreeNode* node = q.front();
        q.pop();

        // process node

        if (node->left) q.push(node->left);
        if (node->right) q.push(node->right);
    }
}
```

## Level-aware BFS

Algorithm:
- Push root to queue.
- While queue is not empty:
    - Check queue size in advance and for 'size' times:
        - Dequeue node, process it.
        - Enqueue left and right children.

```cpp
void levelAwareBfs(TreeNode* root) {
    if (!root) return;

    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        int size = q.size();

        while (size--) {
            TreeNode* node = q.front();
            q.pop();

            // process node (of same level)

            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
    }
}
```

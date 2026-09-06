# DFS (Binary Tree)

### Notes:
- DFS is naturally recursive (pre-order, in-order, post-order)
- can also be implemented iteratively
- uses stack (call stack for recursive, explicit stack for iterative)


- Time: O(n)
- Space: O(h) -> O(log n) average, O(n) worst case

## Recursive

### Pre-order (top-down)

```cpp
void dfs(TreeNode* root) {
    if (!root) return;
    // process node
    dfs(root->left);
    dfs(root->right);
}
```

### In-order

Gives sorted order for a BST.

```cpp
void dfs(TreeNode* root) {
    if (!root) return;
    dfs(root->left);
    // process node
    dfs(root->right);
}
```

### Post-order (bottom-up)

Example: find depth of a binary tree.

```cpp
void dfs(TreeNode* root) {
    if (!root) return;
    dfs(root->left);
    dfs(root->right);
    // process node
}
```

## Iterative

- Time: O(n)
- Space: O(h) -> O(log n) average, O(n) worst case

### Pre-order (top-down) - default

Algorithm:
- Push root to stack.
- While stack is not empty:
    - Pop node, process it.
    - Push right child, then left child (so left is processed first).

```cpp
void dfs_iterative_preorder(TreeNode* root) {
    if (!root) return;

    stack<TreeNode*> st;
    st.push(root);

    while (!st.empty()) {
        TreeNode* node = st.top();
        st.pop();

        // process node

        // push right first so left is processed first
        if (node->right) st.push(node->right);
        if (node->left) st.push(node->left);
    }
}
```

### In-order

Gives sorted order for a BST. Used in: Validate Binary Search Tree.

Algorithm:
- Go as left as possible, pushing nodes onto the stack.
- When reaching nullptr, pop from the stack, process the node, then go right.

```cpp
void dfs_iterative_inorder(TreeNode* root) {
    stack<TreeNode*> s;
    TreeNode* curr = root;

    while (!s.empty() || curr) {
        while (curr) {
            s.push(curr);
            // go left as deep as possible
            curr = curr->left;
        }

        curr = s.top();
        s.pop();

        // process node

        // move to right subtree
        curr = curr->right;
    }
}
```

### Post-order (bottom-up)

Used in: Balanced Binary Tree, Diameter of a Binary Tree.

Algorithm:
- Push leftmost nodes to stack.
- Use lastVisited pointer to know if right child is already processed.
- Process node after left and right children.

```cpp
void dfs_iterative_postorder(TreeNode* root) {
    if (!root) return;

    stack<TreeNode*> s;
    TreeNode* lastVisited = nullptr;
    TreeNode* curr = root;

    while (!s.empty() || curr) {
        if (curr) {
            s.push(curr);
            // go left as deep as possible
            curr = curr->left;
        } else {
            TreeNode* peekNode = s.top();
            // if right child exists and hasn't been visited yet
            if (peekNode->right && lastVisited != peekNode->right) {
                curr = peekNode->right;
            } else {

                // process node

                lastVisited = peekNode;
                s.pop();
            }
        }
    }
}
```

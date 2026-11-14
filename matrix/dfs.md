# DFS (2D Matrix)

- Time: O(n * m)
- Space: O(n * m)

### Notes:
- Mark visited when pushing to stack (not when popping) to avoid duplicate insertions.
- Check boundaries/eligibility before pushing to stack (not after popping) to avoid invalid insertions.
- Add problem-specific eligibility check, otherwise every cell is traversable.
- Use iterative DFS when grid dimensions can be large, recursive DFS can cause stack overflow.

### Iterative

```cpp
void dfsIterative(vector<vector<int>>& grid, vector<vector<bool>>& visited, int r, int c) {
    int n = grid.size(), m = grid[0].size();
    const vector<pair<int,int>> dir = {{1,0}, {-1,0}, {0,1}, {0,-1}};
    stack<pair<int,int>> st;
    st.push({r, c});
    visited[r][c] = true;

    while (!st.empty()) {
        auto [x, y] = st.top();
        st.pop();

        // Process current cell

        for (const auto& [dx, dy] : dir) {
            int nx = x + dx;
            int ny = y + dy;
            if (nx >= 0 && nx < n && ny >= 0 && ny < m && !visited[nx][ny] && /* eligibility-check */) {
                st.push({nx, ny});
                visited[nx][ny] = true;
            }
        }
    }
}
```

### Recursive

- Visited and eligibility check is done at function entry for cleaner code, but can also be done before recursive calls to avoid unnecessary function calls.

```cpp
const pair<int,int> dir[] = {{1,0}, {-1,0}, {0,1}, {0,-1}};

void dfs(vector<vector<int>>& grid, vector<vector<bool>>& visited, int x, int y) {
    int n = grid.size(), m = grid[0].size();
    if (x < 0 || x >= n || y < 0 || y >= m || visited[x][y] || /* eligibility-check */) return;
    visited[x][y] = true;

    // Process current cell

    for (const auto& [dx, dy] : dir) {
        dfs(grid, visited, x + dx, y + dy);
    }
}
```

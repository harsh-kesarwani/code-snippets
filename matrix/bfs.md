# BFS (2D Matrix)

- Time: O(n * m)
- Space: O(n * m)

### Notes:
- Mark visited when pushing to queue (not when popping) to avoid inserting duplicate/already-visited cells.
- Check boundaries/eligibility before pushing to queue (not after popping) to avoid inserting invalid cells.
- Add problem-specific eligibility check, otherwise every cell is traversable.

```cpp
void bfs(vector<vector<int>>& grid, vector<vector<bool>>& visited, int r, int c) {
    int n = grid.size(), m = grid[0].size();
    const vector<pair<int,int>> dir = {{1,0}, {-1,0}, {0,1}, {0,-1}};
    queue<pair<int,int>> q;
    q.push({r, c});
    visited[r][c] = true;

    while (!q.empty()) {
        auto [x, y] = q.front();
        q.pop();
        
        // Process current cell
        
        for (const auto& [dx, dy] : dir) {
            int nx = x + dx;
            int ny = y + dy;
            if (nx >= 0 && nx < n && ny >= 0 && ny < m && !visited[nx][ny] && /* eligibility-check */) {
                q.push({nx, ny});
                visited[nx][ny] = true;
            }
        }
    }
}
```
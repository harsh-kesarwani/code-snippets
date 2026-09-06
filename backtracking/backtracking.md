# Backtracking

Generic template: try each choice, recurse, then undo it (backtrack) to explore
all candidates.

- Time: O(b^d) branches^depth (problem-dependent)
- Space: O(d) recursion depth

```cpp
vector<vector<int>> solve(vector<int>& input) {
    vector<vector<int>> ans;
    vector<int> curr;
    vector<int> visited;
    backtrack(input, ans, curr, visited);
    return ans;
}

void backtrack(const vector<int>& nums, vector<vector<int>>& ans,
               vector<int>& curr, vector<int>& visited) {
    if (/* end condition */) {
        ans.push_back(curr);
        return;
    }
    for (int i = 0; i < nums.size(); i++) {
        // skip condition
        curr.push_back(nums[i]);
        backtrack(nums, ans, curr, visited);
        curr.pop_back();
    }
}
```

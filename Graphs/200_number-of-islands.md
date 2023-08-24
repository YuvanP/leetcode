[[200] - Number of Islands](https://leetcode.com/problems/number-of-islands)

---

- Medium
- [Submission]()
- array, depth-first-search, breadth-first-search, union-find, matrix

---

## Problem Statement

<p>Given an <code>m x n</code> 2D binary grid <code>grid</code> which represents a map of <code>&#39;1&#39;</code>s (land) and <code>&#39;0&#39;</code>s (water), return <em>the number of islands</em>.</p>

<p>An <strong>island</strong> is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> grid = [
  [&quot;1&quot;,&quot;1&quot;,&quot;1&quot;,&quot;1&quot;,&quot;0&quot;],
  [&quot;1&quot;,&quot;1&quot;,&quot;0&quot;,&quot;1&quot;,&quot;0&quot;],
  [&quot;1&quot;,&quot;1&quot;,&quot;0&quot;,&quot;0&quot;,&quot;0&quot;],
  [&quot;0&quot;,&quot;0&quot;,&quot;0&quot;,&quot;0&quot;,&quot;0&quot;]
]
<strong>Output:</strong> 1
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> grid = [
  [&quot;1&quot;,&quot;1&quot;,&quot;0&quot;,&quot;0&quot;,&quot;0&quot;],
  [&quot;1&quot;,&quot;1&quot;,&quot;0&quot;,&quot;0&quot;,&quot;0&quot;],
  [&quot;0&quot;,&quot;0&quot;,&quot;1&quot;,&quot;0&quot;,&quot;0&quot;],
  [&quot;0&quot;,&quot;0&quot;,&quot;0&quot;,&quot;1&quot;,&quot;1&quot;]
]
<strong>Output:</strong> 3
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == grid.length</code></li>
	<li><code>n == grid[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 300</code></li>
	<li><code>grid[i][j]</code> is <code>&#39;0&#39;</code> or <code>&#39;1&#39;</code>.</li>
</ul>


---

## Solution

```cpp
//dfs - beats 99%
class Solution {
public:
    int numIslands(vector<vector<char>>& grid) {
        if(grid.empty()) return 0;

        int island = 0;
        for(int row = 0; row < grid.size(); row++) {
            for(int col = 0; col < grid[0].size(); col++) {
                if(grid[row][col] == '1') {
                    dfs(grid, row, col);
                    island++;
                }
            }
        }
        return island;
    }

private: 
    void dfs(vector<vector<char>> &grid, int row, int col) {
        if(row < 0 || row >= grid.size() || col >= grid[0].size() || grid[row][col] != '1')
            return;
        

        grid[row][col] = '2';

        dfs(grid, row + 1, col);
        dfs(grid, row, col + 1);
        dfs(grid, row - 1, col);
        dfs(grid, row, col - 1);
    }
};


//bfs - beats 88%

class Solution {
public:
    int numIslands(vector<vector<char>>& grid) {
        int n = grid.size();
        if(n == 0) return 0;

        int m = grid[0].size();

        stack<pair<int, int>> s;
        int islands = 0;
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < m; j++) {
                if(grid[i][j] == '1') {
                    islands ++;
                    s.push(make_pair(i, j));

                    while(!s.empty()) {
                        int x = s.top().first;
                        int y = s.top().second;
                        s.pop();
                        
                        grid[x][y] = '0';

                        if(y + 1 < m && grid[x][y + 1] == '1')
                            s.push(make_pair(x, y + 1));
                        
                        if(x + 1 < n && grid[x + 1][y] == '1')
                            s.push(make_pair(x + 1, y));
                        
                        if(y - 1 >= 0 && grid[x][y - 1] == '1')
                            s.push(make_pair(x, y - 1));
                        
                        if(x - 1 >= 0 && grid[x - 1][y] == '1')
                            s.push(make_pair(x - 1, y));
                    }
                }
            }
        }
        return islands;
    }
};
```

---

## Notes


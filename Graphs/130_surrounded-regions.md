[[130] - Surrounded Regions](https://leetcode.com/problems/surrounded-regions)

---

- Medium
- [Submission]()
- array, depth-first-search, breadth-first-search, union-find, matrix

---

## Problem Statement

<p>Given an <code>m x n</code> matrix <code>board</code> containing <code>&#39;X&#39;</code> and <code>&#39;O&#39;</code>, <em>capture all regions that are 4-directionally&nbsp;surrounded by</em> <code>&#39;X&#39;</code>.</p>

<p>A region is <strong>captured</strong> by flipping all <code>&#39;O&#39;</code>s into <code>&#39;X&#39;</code>s in that surrounded region.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/19/xogrid.jpg" style="width: 550px; height: 237px;" />
<pre>
<strong>Input:</strong> board = [[&quot;X&quot;,&quot;X&quot;,&quot;X&quot;,&quot;X&quot;],[&quot;X&quot;,&quot;O&quot;,&quot;O&quot;,&quot;X&quot;],[&quot;X&quot;,&quot;X&quot;,&quot;O&quot;,&quot;X&quot;],[&quot;X&quot;,&quot;O&quot;,&quot;X&quot;,&quot;X&quot;]]
<strong>Output:</strong> [[&quot;X&quot;,&quot;X&quot;,&quot;X&quot;,&quot;X&quot;],[&quot;X&quot;,&quot;X&quot;,&quot;X&quot;,&quot;X&quot;],[&quot;X&quot;,&quot;X&quot;,&quot;X&quot;,&quot;X&quot;],[&quot;X&quot;,&quot;O&quot;,&quot;X&quot;,&quot;X&quot;]]
<strong>Explanation:</strong> Notice that an &#39;O&#39; should not be flipped if:
- It is on the border, or
- It is adjacent to an &#39;O&#39; that should not be flipped.
The bottom &#39;O&#39; is on the border, so it is not flipped.
The other three &#39;O&#39; form a surrounded region, so they are flipped.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> board = [[&quot;X&quot;]]
<strong>Output:</strong> [[&quot;X&quot;]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == board.length</code></li>
	<li><code>n == board[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 200</code></li>
	<li><code>board[i][j]</code> is <code>&#39;X&#39;</code> or <code>&#39;O&#39;</code>.</li>
</ul>


---

## Solution

```cpp
class Solution {
public:
    void solve(vector<vector<char>>& board) {
        int m = board.size();
        int n = board[0].size();

        for(int i = 0; i < m; i++) {
            if(board[i][0] == 'O')
                dfs(board, i, 0);
            if(board[i][n - 1] == 'O')
                dfs(board, i, n - 1);
        }

        for(int j = 0; j < n; j++) {
            if(board[0][j] == 'O')
                dfs(board, 0, j);
            if(board[m - 1][j] == 'O')
                dfs(board, m - 1, j);
        }

        for(int i = 0; i < m; i++) {
            for(int j = 0; j < n; j++) {
                if(board[i][j] == 'O')
                    board[i][j] = 'X';
                if(board[i][j] == '#')
                    board[i][j] = 'O';
            }
        }  
    }

private:
    void dfs(vector<vector<char>>& board, int i, int j) {
        if(i < 0 || j < 0 || i >= board.size() || j >= board[0].size() || board[i][j] != 'O') return;
        board[i][j] = '#';
        dfs(board, i - 1, j);
        dfs(board, i + 1, j);
        dfs(board, i, j - 1);
        dfs(board, i, j + 1);
    }
};
```

---

## Notes


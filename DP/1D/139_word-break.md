[[139] - Word Break](https://leetcode.com/problems/word-break)

---

- Medium
- [Submission]()
- array, hash-table, string, dynamic-programming, trie, memoization

---

## Problem Statement

<p>Given a string <code>s</code> and a dictionary of strings <code>wordDict</code>, return <code>true</code> if <code>s</code> can be segmented into a space-separated sequence of one or more dictionary words.</p>

<p><strong>Note</strong> that the same word in the dictionary may be reused multiple times in the segmentation.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;leetcode&quot;, wordDict = [&quot;leet&quot;,&quot;code&quot;]
<strong>Output:</strong> true
<strong>Explanation:</strong> Return true because &quot;leetcode&quot; can be segmented as &quot;leet code&quot;.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;applepenapple&quot;, wordDict = [&quot;apple&quot;,&quot;pen&quot;]
<strong>Output:</strong> true
<strong>Explanation:</strong> Return true because &quot;applepenapple&quot; can be segmented as &quot;apple pen apple&quot;.
Note that you are allowed to reuse a dictionary word.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;catsandog&quot;, wordDict = [&quot;cats&quot;,&quot;dog&quot;,&quot;sand&quot;,&quot;and&quot;,&quot;cat&quot;]
<strong>Output:</strong> false
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 300</code></li>
	<li><code>1 &lt;= wordDict.length &lt;= 1000</code></li>
	<li><code>1 &lt;= wordDict[i].length &lt;= 20</code></li>
	<li><code>s</code> and <code>wordDict[i]</code> consist of only lowercase English letters.</li>
	<li>All the strings of <code>wordDict</code> are <strong>unique</strong>.</li>
</ul>


---

## Solution

```cpp
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        vector<bool> dp(s.size() + 1, false);
        dp[s.size()] = true;

        for(int i = s.size() - 1; i >= 0; i--) {
            for(auto w : wordDict) {
                if(i + w.size() <= s.size() && s.substr(i, w.size()) == w)
                    dp[i] = dp[i + w.size()];
                if(dp[i])
                    break;
            }
        }
        return dp[0];
    }
};
```

---

## Notes

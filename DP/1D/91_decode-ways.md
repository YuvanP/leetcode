[[91] - Decode Ways](https://leetcode.com/problems/decode-ways)

---

- Medium
- [Submission]()
- string, dynamic-programming

---

## Problem Statement

<p>A message containing letters from <code>A-Z</code> can be <strong>encoded</strong> into numbers using the following mapping:</p>

<pre>
&#39;A&#39; -&gt; &quot;1&quot;
&#39;B&#39; -&gt; &quot;2&quot;
...
&#39;Z&#39; -&gt; &quot;26&quot;
</pre>

<p>To <strong>decode</strong> an encoded message, all the digits must be grouped then mapped back into letters using the reverse of the mapping above (there may be multiple ways). For example, <code>&quot;11106&quot;</code> can be mapped into:</p>

<ul>
	<li><code>&quot;AAJF&quot;</code> with the grouping <code>(1 1 10 6)</code></li>
	<li><code>&quot;KJF&quot;</code> with the grouping <code>(11 10 6)</code></li>
</ul>

<p>Note that the grouping <code>(1 11 06)</code> is invalid because <code>&quot;06&quot;</code> cannot be mapped into <code>&#39;F&#39;</code> since <code>&quot;6&quot;</code> is different from <code>&quot;06&quot;</code>.</p>

<p>Given a string <code>s</code> containing only digits, return <em>the <strong>number</strong> of ways to <strong>decode</strong> it</em>.</p>

<p>The test cases are generated so that the answer fits in a <strong>32-bit</strong> integer.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;12&quot;
<strong>Output:</strong> 2
<strong>Explanation:</strong> &quot;12&quot; could be decoded as &quot;AB&quot; (1 2) or &quot;L&quot; (12).
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;226&quot;
<strong>Output:</strong> 3
<strong>Explanation:</strong> &quot;226&quot; could be decoded as &quot;BZ&quot; (2 26), &quot;VF&quot; (22 6), or &quot;BBF&quot; (2 2 6).
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;06&quot;
<strong>Output:</strong> 0
<strong>Explanation:</strong> &quot;06&quot; cannot be mapped to &quot;F&quot; because of the leading zero (&quot;6&quot; is different from &quot;06&quot;).
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 100</code></li>
	<li><code>s</code> contains only digits and may contain leading zero(s).</li>
</ul>


---

## Solution

```cpp
//Recursion
class Solution {
public:
    int numDecodings(string s) {
        int res = 0;
        res = rec(s, 0);
        return res;
    }

private:
    int rec(string &s, int pos) {
        if(pos == s.size()) return 1;

        if(s[pos] == '0') return 0;

        if(pos == s.size() - 1) return 1;

        string b = s.substr(pos, 2);

        int way1 = rec(s, pos + 1);
        int way2 = 0;

        if(stoi(b) <= 26 && stoi(b) > 0) way2 = rec(s, pos + 2);

        return way1 + way2;
    }
};

//Memoization
class Solution {
public:
    int numDecodings(string s) {
        vector<int> hg(s.size() + 1, 0);
        int res = 0;
        res = rec(s, 0, hg);
        return res;
    }

private:
    int rec(string &s, int pos, vector<int> &hg) {
        if(pos == s.size()) return 1;

        if(s[pos] == '0') return 0;

        if(pos == s.size() - 1) return 1;

        if(hg[pos] > 0) return hg[pos];

        string b = s.substr(pos, 2);

        int way1 = rec(s, pos + 1, hg);
        int way2 = 0;

        if(stoi(b) <= 26 && stoi(b) > 0) way2 = rec(s, pos + 2, hg);

        hg[pos] = way1 + way2;
        return hg[pos];
    }
};

//DP
class Solution {
public:
    int numDecodings(string s) {
        vector<int> dp(s.size() + 1);
        dp[0] = 1;
        if(s[0] == '0') dp[1] = 0;
        else dp[1] = 1;
        
        for(int i = 2; i <= s.size(); i++) {
            int way1, way2;

            if(s[i - 1] == '0') way1 = 0;

            else way1 = dp[i - 1];

            if(stoi(s.substr(i - 2, 2)) <= 26 && stoi(s.substr(i - 2, 2)) > 0 && s[i - 2] != '0')
                way2 = dp[i - 2];
            
            else way2 = 0;

            dp[i] = way1 + way2;
        }
        return dp[s.size()];
    }
};
```

---

## Notes


[[5] - Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring)

---

- Medium
- [Submission]()
- string, dynamic-programming

---

## Problem Statement

<p>Given a string <code>s</code>, return <em>the longest</em> <span data-keyword="palindromic-string"><em>palindromic</em></span> <span data-keyword="substring-nonempty"><em>substring</em></span> in <code>s</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;babad&quot;
<strong>Output:</strong> &quot;bab&quot;
<strong>Explanation:</strong> &quot;aba&quot; is also a valid answer.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;cbbd&quot;
<strong>Output:</strong> &quot;bb&quot;
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 1000</code></li>
	<li><code>s</code> consist of only digits and English letters.</li>
</ul>


---

## Solution

```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        string res = "";
        int len = 0, i = 0, start = 0;

        while(i < s.size()) {
            int l = i, r = i;

            while(r + 1 < s.size() && s[r] == s[r + 1]) r++;
            i = r + 1;

            while(l - 1 >= 0 && r + 1 < s.size() && s[l - 1] == s[r + 1]) {
                l--;
                r++;
            }

            if(r - l + 1 > len) {
                len = r - l + 1;
                start = l;
            }
        }
        return s.substr(start, len);
    }
};
```

---

## Notes


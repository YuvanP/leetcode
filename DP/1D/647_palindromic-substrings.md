[[647] - Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings)

---

- Medium
- [Submission]()
- string, dynamic-programming

---

## Problem Statement

<p>Given a string <code>s</code>, return <em>the number of <strong>palindromic substrings</strong> in it</em>.</p>

<p>A string is a <strong>palindrome</strong> when it reads the same backward as forward.</p>

<p>A <strong>substring</strong> is a contiguous sequence of characters within the string.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;abc&quot;
<strong>Output:</strong> 3
<strong>Explanation:</strong> Three palindromic strings: &quot;a&quot;, &quot;b&quot;, &quot;c&quot;.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;aaa&quot;
<strong>Output:</strong> 6
<strong>Explanation:</strong> Six palindromic strings: &quot;a&quot;, &quot;a&quot;, &quot;a&quot;, &quot;aa&quot;, &quot;aa&quot;, &quot;aaa&quot;.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 1000</code></li>
	<li><code>s</code> consists of lowercase English letters.</li>
</ul>


---

## Solution

```cpp
class Solution {
public:
    int countSubstrings(string s) {
        int count = 0, l = 0, r = 0, i = 0;
        for(int i = 0; i < s.size(); i++) {
            l = i, r = i + 1;
            while(l >= 0 && r < s.size() && s[r] == s[l]) {
                count++;
                r++;
                l--;
            }  
            l = i, r = i;
            while(l >= 0 && r < s.size() && s[r] == s[l]) {
                count++;
                r++;
                l--;
            }
        }
        return count;
    }
};
```

---

## Notes


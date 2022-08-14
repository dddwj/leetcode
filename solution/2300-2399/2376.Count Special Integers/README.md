# [2376. 统计特殊整数](https://leetcode.cn/problems/count-special-integers)

[English Version](/solution/2300-2399/2376.Count%20Special%20Integers/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->

<p>如果一个正整数每一个数位都是 <strong>互不相同</strong>&nbsp;的，我们称它是 <strong>特殊整数</strong> 。</p>

<p>给你一个 <strong>正</strong>&nbsp;整数&nbsp;<code>n</code>&nbsp;，请你返回区间<em>&nbsp;</em><code>[1, n]</code>&nbsp;之间特殊整数的数目。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<b>输入：</b>n = 20
<b>输出：</b>19
<b>解释：</b>1 到 20 之间所有整数除了 11 以外都是特殊整数。所以总共有 19 个特殊整数。
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<b>输入：</b>n = 5
<b>输出：</b>5
<b>解释：</b>1 到 5 所有整数都是特殊整数。
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<b>输入：</b>n = 135
<b>输出：</b>110
<b>解释：</b>从 1 到 135 总共有 110 个整数是特殊整数。
不特殊的部分数字为：22 ，114 和 131 。</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 2 * 10<sup>9</sup></code></li>
</ul>

## 解法

<!-- 这里可写通用的实现逻辑 -->

<!-- tabs:start -->

### **Python3**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```python
class Solution:
    def countSpecialNumbers(self, n: int) -> int:
        def A(m, n):
            return 1 if n == 0 else A(m, n - 1) * (m - n + 1)

        vis = [False] * 10
        ans = 0
        digits = [int(c) for c in str(n)[::-1]]
        m = len(digits)
        for i in range(1, m):
            ans += 9 * A(9, i - 1)
        for i in range(m - 1, -1, -1):
            v = digits[i]
            j = 1 if i == m - 1 else 0
            while j < v:
                if not vis[j]:
                    ans += A(10 - (m - i), i)
                j += 1
            if vis[v]:
                break
            vis[v] = True
            if i == 0:
                ans += 1
        return ans
```

### **Java**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```java
class Solution {
    public int countSpecialNumbers(int n) {
        List<Integer> digits = new ArrayList<>();
        while (n != 0) {
            digits.add(n % 10);
            n /= 10;
        }
        int m = digits.size();
        int ans = 0;
        for (int i = 1; i < m; ++i) {
            ans += 9 * A(9, i - 1);
        }
        boolean[] vis = new boolean[10];
        for (int i = m - 1; i >= 0; --i) {
            int v = digits.get(i);
            for (int j = i == m - 1 ? 1 : 0; j < v; ++j) {
                if (vis[j]) {
                    continue;
                }
                ans += A(10 - (m - i), i);
            }
            if (vis[v]) {
                break;
            }
            vis[v] = true;
            if (i == 0) {
                ++ans;
            }
        }
        return ans;
    }

    private int A(int m, int n) {
        return n == 0 ? 1 : A(m, n - 1) * (m - n + 1);
    }
}
```

### **C++**

```cpp
class Solution {
public:
    int countSpecialNumbers(int n) {
        int ans = 0;
        vector<int> digits;
        while (n) {
            digits.push_back(n % 10);
            n /= 10;
        }
        int m = digits.size();
        vector<bool> vis(10);
        for (int i = 1; i < m; ++i) {
            ans += 9 * A(9, i - 1);
        }
        for (int i = m - 1; ~i; --i) {
            int v = digits[i];
            for (int j = i == m - 1 ? 1 : 0; j < v; ++j) {
                if (!vis[j]) {
                    ans += A(10 - (m - i), i);
                }
            }
            if (vis[v]) {
                break;
            }
            vis[v] = true;
            if (i == 0) {
                ++ans;
            }
        }
        return ans;
    }

    int A(int m, int n) {
        return n == 0 ? 1 : A(m, n - 1) * (m - n + 1);
    }
};
```

### **Go**

```go
func countSpecialNumbers(n int) int {
	digits := []int{}
	for n != 0 {
		digits = append(digits, n%10)
		n /= 10
	}
	m := len(digits)
	vis := make([]bool, 10)
	ans := 0
	for i := 1; i < m; i++ {
		ans += 9 * A(9, i-1)
	}
	for i := m - 1; i >= 0; i-- {
		v := digits[i]
		j := 0
		if i == m-1 {
			j = 1
		}
		for ; j < v; j++ {
			if !vis[j] {
				ans += A(10-(m-i), i)
			}
		}
		if vis[v] {
			break
		}
		vis[v] = true
		if i == 0 {
			ans++
		}
	}
	return ans
}

func A(m, n int) int {
	if n == 0 {
		return 1
	}
	return A(m, n-1) * (m - n + 1)
}
```

### **TypeScript**

```ts

```

### **...**

```


```

<!-- tabs:end -->
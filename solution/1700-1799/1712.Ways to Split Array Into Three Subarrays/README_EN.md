# [1712. Ways to Split Array Into Three Subarrays](https://leetcode.com/problems/ways-to-split-array-into-three-subarrays)

[中文文档](/solution/1700-1799/1712.Ways%20to%20Split%20Array%20Into%20Three%20Subarrays/README.md)

## Description

<p>A split of an integer array is <strong>good</strong> if:</p>

<ul>
	<li>The array is split into three <strong>non-empty</strong> contiguous subarrays - named <code>left</code>, <code>mid</code>, <code>right</code> respectively from left to right.</li>
	<li>The sum of the elements in <code>left</code> is less than or equal to the sum of the elements in <code>mid</code>, and the sum of the elements in <code>mid</code> is less than or equal to the sum of the elements in <code>right</code>.</li>
</ul>

<p>Given <code>nums</code>, an array of <strong>non-negative</strong> integers, return <em>the number of <strong>good</strong> ways to split</em> <code>nums</code>. As the number may be too large, return it <strong>modulo</strong> <code>10<sup>9 </sup>+ 7</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,1,1]
<strong>Output:</strong> 1
<strong>Explanation:</strong> The only good way to split nums is [1] [1] [1].</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,2,2,2,5,0]
<strong>Output:</strong> 3
<strong>Explanation:</strong> There are three good ways of splitting nums:
[1] [2] [2,2,5,0]
[1] [2,2] [2,5,0]
[1,2] [2,2] [5,0]
</pre>

<p><strong>Example 3:</strong></p>

<pre>
<strong>Input:</strong> nums = [3,2,1]
<strong>Output:</strong> 0
<strong>Explanation:</strong> There is no good way to split nums.</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>3 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= nums[i] &lt;= 10<sup>4</sup></code></li>
</ul>

## Solutions

<!-- tabs:start -->

### **Python3**

```python
class Solution:
    def waysToSplit(self, nums: List[int]) -> int:
        mod = 10**9 + 7
        s = list(accumulate(nums))
        ans, n = 0, len(nums)
        for i in range(n - 2):
            j0 = bisect_left(s, s[i] * 2, i + 1, n - 1)
            j1 = bisect_right(s, (s[-1] + s[i]) // 2, j0, n - 1)
            ans += j1 - j0
        return ans % mod
```

### **Java**

```java
class Solution {
    private static final int MOD = (int) 1e9 + 7;

    public int waysToSplit(int[] nums) {
        int n = nums.length;
        int[] s = new int[n];
        s[0] = nums[0];
        for (int i = 1; i < n; ++i) {
            s[i] = s[i - 1] + nums[i];
        }
        int ans = 0;
        for (int i = 0; i < n - 2; ++i) {
            int j0 = lowerBound(s, s[i] * 2, i + 1, n - 1);
            int j1 = lowerBound(s, (s[i] + s[n - 1]) / 2 + 1, j0, n - 1);
            ans = (ans + j1 - j0) % MOD;
        }
        return ans;
    }

    private int lowerBound(int[] s, int x, int left, int right) {
        while (left < right) {
            int mid = (left + right) >> 1;
            if (s[mid] >= x) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return left;
    }
}
```

### **C++**

```cpp
class Solution {
public:
    int waysToSplit(vector<int>& nums) {
        int n = nums.size();
        vector<int> s(n, nums[0]);
        for (int i = 1; i < n; ++i) s[i] = s[i - 1] + nums[i];
        int ans = 0;
        int mod = 1e9 + 7;
        for (int i = 0; i < n - 2; ++i) {
            int j0 = lower_bound(s.begin() + i + 1, s.begin() + n - 1, s[i] * 2) - s.begin();
            int j1 = upper_bound(s.begin() + j0, s.begin() + n - 1, (s[i] + s[n - 1]) / 2) - s.begin();
            ans = (ans + j1 - j0) % mod;
        }
        return ans;
    }
};
```

### \*\*\*\*

```go
func waysToSplit(nums []int) int {
	search := func(s []int, x, left, right int) int {
		for left < right {
			mid := (left + right) >> 1
			if s[mid] >= x {
				right = mid
			} else {
				left = mid + 1
			}
		}
		return left
	}
	var mod int = 1e9 + 7
	n := len(nums)
	s := make([]int, n)
	s[0] = nums[0]
	for i := 1; i < n; i++ {
		s[i] = s[i-1] + nums[i]
	}
	ans := 0
	for i := 0; i < n-2; i++ {
		j0 := search(s, s[i]*2, i+1, n-1)
		j1 := search(s, (s[i]+s[n-1])/2+1, j0, n-1)
		ans += j1 - j0
	}
	ans %= mod
	return ans
}
```

### **...**

```

```

<!-- tabs:end -->

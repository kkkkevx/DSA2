![image](https://github.com/kkkkevx/DSA2/assets/108632304/d2a4a6f9-aad8-4855-bbbd-ca5e739256ad)

## [Solution](https://leetcode.cn/problems/longest-substring-without-repeating-characters/description/)

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        /**
        滑动窗口 

        当有相同的元素时滑动窗口
         */


        Map<Character, Integer> window = new HashMap<>();
        int left = 0, right = 0;
        int res = 0;

        while (right < s.length()) {
            char c = s.charAt(right);
            right++;
            window.put(c, window.getOrDefault(c, 0) + 1);

            while (window.get(c) > 1) {
                // res = Math.max(res, right - left - 1); 不能放这里是因为这时候window里面包含重复的元素
                char d = s.charAt(left);
                left++;
                window.put(d, window.get(d) - 1);
            }
            res = Math.max(res, right - left);
        }

        return res;

    }
}
```

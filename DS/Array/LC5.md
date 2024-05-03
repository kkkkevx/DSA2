![image](https://github.com/kkkkevx/DSA2/assets/108632304/0d9d570c-6374-462a-903f-ebc21c4df6c9)

## [Solution](https://leetcode.cn/problems/longest-palindromic-substring/)

```java
class Solution {
    public String longestPalindrome(String s) {
        // 双指针 注意的点 字符串的奇偶 找最长从中心往两边散 每一个字符都是一次中心
        String res = "";
        for (int i = 0; i < s.length(); i++) {
            String str1 = palindrome(s, i, i);
            String str2 = palindrome(s, i, i + 1);

            res = (res.length() > str1.length()) ? res : str1;
            res = (res.length() > str2.length()) ? res : str2;
        }

        return res;
    }

    private String palindrome(String s, int left, int right) {
        while (left >= 0 && right < s.length()) {
            if (s.charAt(left) == s.charAt(right)) {
                left--;
                right++;
            } else {
                break;
            }
        }

        return s.substring(left + 1, right);
    }
}
```

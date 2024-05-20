![image](https://github.com/kkkkevx/DSA2/assets/108632304/75849e12-52c8-444d-baf0-c37076445bb4)

## [Solution](https://leetcode.cn/problems/two-sum/)

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        // 最优解用hash map 时间和空间都是o（n）
        
        // HashMap<Integer, Integer> record = new HashMap<>(); // (element, index)

        // for (int i = 0; i < nums.length; i++) {
        //     int diff = target - nums[i];
        //     if (record.containsKey(diff)) {
        //         return new int[]{i, record.get(diff)};
        //     }

        //     record.put(nums[i], i);
        // }

        // return new int[]{-1,-1};

        // 双指针解法 空间O(1) 时间o(n)
        // 魔改题目 满足双数之和 返回的是元素并非指针

        Arrays.sort(nums);
        int left = 0, right = nums.length - 1;

        while (left < right) {
            int sum = nums[left] + nums[right];
            if (sum == target) {
                return new int[]{left, right};
            } else if (sum < target) {
                left++;
            } else if (sum > target) {
                right--;
            }
        }

        return new int[]{-1, -1};

    }
}
```

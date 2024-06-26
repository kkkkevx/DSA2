![image](https://github.com/kkkkevx/DSA2/assets/108632304/998d9ebc-362b-4877-abed-d6f4eb4fe13e)

递归： 计算机中居然有递归这么<唯心主义>的算法，定义一个方法，坚定地相信它能完成一项功能，然后递归调用就行，完全没法考虑它到底是怎么实现的 
  - 递归函数 定义他解决了什么问题相信他能够完成 -> base case -> 每个节点在干什么 -> return 值的意义

链表算法： 双指针

数组算法：双指针 -> 滑动窗口（双指针）-> 二分搜索，前缀和， 差分数组 
  - 前缀和：主要适用的场景是原始数组不会被修改的情况下，频繁查询某个区间的累加和。
  - 差分数组：主要适用场景是频繁对原始数组的某个区间的元素进行增减。
    - 涉及到和为 xxx 的连续子数组，就是要考察 前缀和技巧 和哈希表的结合使用了。
  - 滑动窗口：算法技巧主要用来解决子数组问题，比如让你寻找符合某个条件的最长/最短子数组。
    - 模板
  ```java
import java.util.HashMap;
import java.util.Map;

public class Main {
    /* 滑动窗口算法框架 */
    public static void slidingWindow(String s) {
        // 用合适的数据结构记录窗口中的数据，根据具体场景变通
        // 比如说，我想记录窗口中元素出现的次数，就用 map
        // 我想记录窗口中的元素和，就用 int
        Map<Character, Integer> window = new HashMap<>();
        
        int left = 0, right = 0;
        while (right < s.length()) {
            // c 是将移入窗口的字符
            char c = s.charAt(right);
            window.put(c, window.getOrDefault(c, 0) + 1);
            // 增大窗口
            right++;
            // 进行窗口内数据的一系列更新
            // ...

            /*** debug 输出的位置 ***/
            // 注意在最终的解法代码中不要 print
            // 因为 IO 操作很耗时，可能导致超时
            System.out.printf("window: [%d, %d)\n", left, right);
            /********************/
            
            // 判断左侧窗口是否要收缩
            while (left < right && window needs shrink) {
                // d 是将移出窗口的字符
                char d = s.charAt(left);
                window.put(d, window.get(d) - 1);
                // 缩小窗口
                left++;
                // 进行窗口内数据的一系列更新
                // ...
            }
        }
    }

    public static void main(String[] args) {
        slidingWindow("your string here");
    }
}
```
  - 二分搜索：在有序数组中搜索指定元素
    - 模板  
```java
int binary_search(int[] nums, int target) {
    int left = 0, right = nums.length - 1; 
    while(left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1; 
        } else if(nums[mid] == target) {
            // 直接返回
            return mid;
        }
    }
    // 直接返回
    return -1;
}

int left_bound(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1;
        } else if (nums[mid] == target) {
            // 别返回，锁定左侧边界
            right = mid - 1;
        }
    }
    // 判断 target 是否存在于 nums 中
    if (left < 0 || left >= nums.length) {
        return -1;
    }
    // 判断一下 nums[left] 是不是 target
    return nums[left] == target ? left : -1;
}

int right_bound(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1;
        } else if (nums[mid] == target) {
            // 别返回，锁定右侧边界
            left = mid + 1;
        }
    }
    
    // 由于 while 的结束条件是 right == left - 1，且现在在求右边界
    // 所以用 right 替代 left - 1 更好记
    if (right < 0 || right >= nums.length) {
        return -1;
    }
    return nums[right] == target ? right : -1;
}

```

![image](https://github.com/kkkkevx/DSA2/assets/108632304/f754e867-4c4f-4a0e-b6df-cd5831245105)

**二叉树**
  - 前中后序是遍历二叉树过程中处理每一个节点的三个特殊时间点，绝不仅仅是三个顺序不同的 List：
    - 前序位置的代码在刚刚进入一个二叉树节点的时候执行；
    - 后序位置的代码在将要离开一个二叉树节点的时候执行；
    - 中序位置的代码在一个二叉树节点左子树都遍历完，即将开始遍历右子树的时候执行。
  - 综上，遇到一道二叉树的题目时的通用思考过程是：
    - 是否可以通过遍历一遍二叉树得到答案？如果可以，用一个 traverse 函数配合外部变量来实现。
    - 是否可以定义一个递归函数，通过子问题（子树）的答案推导出原问题的答案？如果可以，写出这个递归函数的定义，并充分利用这个函数的返回值。
    - 无论使用哪一种思维模式，你都要明白二叉树的每一个节点需要做什么，需要在什么时候（前中后序）做。
    - 
动归/DFS/回溯算法都可以看做二叉树问题的扩展，只是它们的关注点不同：

动态规划算法属于分解问题的思路，它的关注点在整棵「子树」。

回溯算法属于遍历的思路，它的关注点在节点间的「树枝」。

DFS 算法属于遍历的思路，它的关注点在单个「节点」。


会议室分配问题是一个经典的算法题目，通常通过扫描线算法或使用最小堆来解决。题目通常描述如下：

给定一组会议时间的区间 [start, end]，求最少需要多少个会议室才能安排所有会议。

示例
lua
复制代码
输入: [[0, 30], [5, 10], [15, 20]]
输出: 2

输入: [[7, 10], [2, 4]]
输出: 1
解决方案
我们可以使用最小堆来追踪当前会议结束的时间，步骤如下：

- 按照会议的开始时间排序。

- 初始化一个最小堆，将第一个会议的结束时间加入堆。

- 对于每一个会议：

  - 检查堆顶的最小结束时间是否小于等于当前会议的开始时间。如果是，说明这个会议室可以重新分配给当前会议，将堆顶元素移除，并将当前会议的结束时间加入堆。

  - 如果不是，说明需要一个新的会议室，将当前会议的结束时间加入堆。

- 最小堆的大小就是所需会议室的数量。


```java
import java.util.*;

public class MeetingRooms {
    public static int minMeetingRooms(int[][] intervals) {
        if (intervals == null || intervals.length == 0) {
            return 0;
        }

        // 按照会议的开始时间排序
        Arrays.sort(intervals, Comparator.comparingInt(a -> a[0]));

        // 使用最小堆来追踪会议结束时间
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();

        // 将第一个会议的结束时间加入堆
        minHeap.add(intervals[0][1]);

        for (int i = 1; i < intervals.length; i++) {
            // 如果当前会议的开始时间大于等于堆顶的结束时间，说明可以重用会议室
            if (intervals[i][0] >= minHeap.peek()) {
                minHeap.poll();
            }

            // 将当前会议的结束时间加入堆
            minHeap.add(intervals[i][1]);
        }

        // 堆的大小即为所需会议室的数量
        return minHeap.size();
    }

    public static void main(String[] args) {
        int[][] intervals1 = {{0, 30}, {5, 10}, {15, 20}};
        int[][] intervals2 = {{7, 10}, {2, 4}};
        
        System.out.println(minMeetingRooms(intervals1)); // 输出: 2
        System.out.println(minMeetingRooms(intervals2)); // 输出: 1
    }
}
```

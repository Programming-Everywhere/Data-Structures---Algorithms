# Greedy - 贪心思想
1. [(455) Assign Cookies](https://leetcode.com/problems/assign-cookies/)
2. [435. Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/description/)
3. [452. Minimum Number of Arrows to Burst Balloons](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/description/)
# 1. (455) Assign Cookies
[leetcode](https://leetcode.com/problems/assign-cookies/)
```java
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        /**
        Assign cookie starting from the child with less greediness
        to gratify max number of kids/
        */
        Arrays.sort(g);
        Arrays.sort(s);
        int i = 0, j = 0;
        int count = 0;
        while(i < g.length && j < s.length) {
            if(g[i] <= s[j]) {
                count++;
                i++;
            }
            j++;
        }
        return count;
    }
}
```
# 2 (435). Non-overlapping Intervals
[leetcode](https://leetcode.com/problems/non-overlapping-intervals/description/)
```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        /**
        1)核心思想： sort 这个array 
        2)然后三个ptr： preEnd， nextStart，nextEnd
        3)然后检查preEnd和nextStart的大小，只有 nextStart >=  preEnd， 我们就数数+1，然后preEnd 更新到nextEnd，这样依次类推
        4)最有用总长度 减去 数数,
        5)这个就是需要减去的结果。
        */
        if (intervals == null || intervals.length == 0) return 0;
        Arrays.sort(intervals, (a, b) -> a[1]-b[1]);
    
        int count = 1;
        int preEnd = intervals[0][1];
        for(int i = 1; i < intervals.length; i++) {
            int nextStart = intervals[i][0];
            int nextEnd = intervals[i][1];
            if(nextStart >= preEnd) { // no overlap
                preEnd = nextEnd;
                count++;
            }
        }
        return intervals.length - count;
    }
}
```
# 3. (452) Minimum Number of Arrows to Burst Balloons
[leetcode](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/description/)
```java
/**
核心思想：跟上题一样，sort y-axis，然后比较右和下个左，如果大 不管，如果小 就arrow++，因为不会沾到下个气球，并且把指标发在这个气球的右边，对比下一个。
*/
class Solution {
    public int findMinArrowShots(int[][] points) {
        /**[start,end]
           [10, 16], 
           [2,  8],
           [1,  6],
           [7,  12]]
           
           [
           [1,  6],
             [2,  8],
                 [7,  12]
                     [10, 16]]
           ]
        */
        if(points == null || points.length == 0) return 0;
        Arrays.sort(points, (a, b) -> a[1]- b[1]);
        
        int preEnd = points[0][1];
        int count = 1;
        for(int i = 1; i < points.length; i++) {
            
            int nextStart = points[i][0];
            if(preEnd < nextStart) {
                count++;
                preEnd = points[i][1];
            }
        }
        return count;
    }
}
```
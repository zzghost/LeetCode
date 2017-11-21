# Largest Rectangle in Histogram
## Description
Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

For example,
Given heights = `[2,1,5,6,2,3]`,
return `10`.
## Solution  
1. Divide and Conquer  
a. Use *[Segment Tree](http://www.geeksforgeeks.org/segment-tree-set-1-range-minimum-query/)* to find the minimal value.**(when the array is very large, it will get Stack Overflow error)**  
**Complexity: Time O(nlogn), Space 2 * Math.pow(2, log2(n)) - 1.**
```java
/*
 * 1. construct segment tree, leaf node is the bar's index,Internal node stores the minimal value's index.
 * 2. find the minimum value in the given array.then the max area is maximum of following three values:
 *  + Maximum area in left side of minimum value
 *  + Maximum area in right size of minimum value
 *  + number of bars multiplied by minimum value.
 * 3. the left and right side can be calculated recursively.
 */
class Solution {
    int[] st;
    public int getMin(int[] heights, int x, int y){
        if(x == -1) return y;
        if(y == -1) return x;
        return heights[x] < heights[y] ? x : y;
    }
    public int constructUtil(int[] heights, int ss, int se, int idx){
        if(ss == se){
            st[idx] = ss;
            return st[idx];
        }
        int mid = (se - ss) / 2 + ss;
        st[idx] = getMin(heights, constructUtil(heights, ss, mid, 2 * idx + 1), constructUtil(heights, mid + 1, se, 2 * idx + 2));
        return st[idx];
    }
    public void constructST(int[] heights){
        int n = heights.length;
        int x = (int) Math.ceil(Math.log(n) / Math.log(2));
        int size = 2 * (int)Math.pow(2, x) - 1;
        st = new int[size];
        constructUtil(heights, 0, n - 1, 0);
    }
    public int RMQUtil(int[] heights, int ss, int se, int qs, int qe, int idx){
        if(qs <= ss && qe >= se){
            return st[idx];
        }
        if(qe < ss || qs > se){
            return -1;
        }
        int mid = (se - ss) / 2 + ss;
        return getMin(heights, RMQUtil(heights, ss, mid, qs, qe, 2 * idx + 1),
                      RMQUtil(heights, mid + 1, se, qs, qe, 2 * idx + 2));
    }

    public int RMQ(int[] heights, int qs, int qe){
        if(qs < 0 || qe > heights.length - 1 || qs > qe)
            return -1;
        return RMQUtil(heights, 0, heights.length -1, qs, qe, 0);
    }
    public int getMax(int x, int y, int z){
        return Math.max(x, Math.max(y, z));
    }

    public int getMaxRect(int[] heights, int l, int r){
        if(l == r) return heights[l];
        if(l > r) return Integer.MIN_VALUE;
        int m = RMQ(heights, l, r);
        return getMax(getMaxRect(heights, l, m - 1),
                      getMaxRect(heights, m + 1, r),
                      (r - l + 1) * heights[m]);
    }
    public int getMaxArea(int[] heights){
        constructST(heights);
        return getMaxRect(heights, 0, heights.length - 1);
    }
    public int largestRectangleArea(int[] heights) {
        if(heights == null || heights.length == 0)
            return 0;
        return getMaxArea(heights);   
    }
}
```
b. Basic Divide and Conquer(**Accepted**)  
Calculate the area in a small interval, and then in a larger.  
Divide the heights array into two pieces recursively.Select the maximum value from left part, right part, the overall part.
```java
/*
 * Use two pointers to go left and right.
 * There's a max area interval: [op_lower..op_upper].
 * If j meets op_upper and i has not reached.Then j will stand still until i reached op_lower.
 * The end condition is i or j reached out of the boundary.
 */
class Solution {
    public int getMax(int x, int y, int z){
        return Math.max(x, Math.max(y, z));
    }
    //find the max area in interval[l .. r]
    public int maxAreaCombine(int[] heights, int l, int m, int r){
        //i and j are two pointers, go left and go right.
        int i = m, j = m + 1;
        //h stores the current lowest bar.
        int h = Math.min(heights[i], heights[j]), area = 0;
        while(i >= l && j <= r){
            h = Math.min(h, Math.min(heights[i], heights[j]));
            area = Math.max(area, (j - i + 1) * h);
            if(i == l)
                ++j;
            else if(j == r)
                --i;
            else{
                if(heights[i - 1] > heights[j + 1])
                    --i;
                else
                    ++j;
            }
        }
        return area;
    }
    public int getMaxArea(int[] heights, int l, int r){
        if(l == r)
            return heights[l];
        int m = (r - l) / 2 + l;
        //find max area from [l..m], [m+1, r], [l, r]
        return getMax(getMaxArea(heights, l, m), getMaxArea(heights, m + 1, r) , maxAreaCombine(heights, l, m, r));
    }
    public int largestRectangleArea(int[] heights) {
        if(heights == null || heights.length == 0)
            return 0;
        return getMaxArea(heights, 0, heights.length - 1);
    }
}
```
2. Use *Stack*(Linear Time)  
From the first bar, push the bars which can form the ascending order until it meets the first descending bar `y`.  
In the stack ,there's a first bar in the stack which is smaller than y, call it `m - 1`, the next is `m`. Call the top of the bar `k`. Now we calculate the `m to k` areas and select the largest.Each rectangular, height is the top of the stack, width is current index to the second top of the stack.   
We can see that the stack stores the index of the possible height.  
See the chinese article written by Liren Chen for details in [this link](https://mp.weixin.qq.com/s?__biz=MjM5ODIzNDQ3Mw==&mid=2649965580&idx=1&sn=6c5da010852f54ac917cd65b71dd512b&scene=2&srcid=0628D20JTralYPgZItmYEeTo&from=timeline&isappinstalled=0#wechat_redirect).   
**Complexity: Time O(n), Space O(n).**
```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        if(heights == null || heights.length == 0)
            return 0;
        int n = heights.length, maxArea = heights[0];
        Stack<Integer> s = new Stack<Integer>();
        for(int i = 0; i <= n; i++){
            int h = (i == n) ? 0 : heights[i];
            if(s.isEmpty() || h >= heights[s.peek()]){
                s.push(i);
            }
            else{
                int tp = s.pop();
                maxArea = Math.max(maxArea, heights[tp] * (s.isEmpty() ? i : (i - 1 - s.peek())));
                i--;
            }
        }
        return maxArea;
    }
}
```

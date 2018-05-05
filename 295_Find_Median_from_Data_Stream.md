# Find Median from Data Stream

## Description
Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.

Examples:
``[2,3,4]`` , the median is `3`

``[2,3]``, the median is `(2 + 3) / 2 = 2.5`

Design a data structure that supports the following two operations:

+ void addNum(int num) - Add a integer number from the data stream to the data structure.
+ double findMedian() - Return the median of all elements so far.

For example:
```
addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3)
findMedian() -> 2
```
## Solution
MaxHeap and MinHeap.  
The MaxHeap stores the first-half elements, while the MinHeap stores another.  
There are 3 cases:  
1) MaxHeap.size() == MinHeap.size(): we should decide which heap to store.  
2) MaxHeap.size() - MinHeap.size() == 1: compare the top element of MaxHeap, regulate the heap.  
3) MinHeap.size() - MaxHeap.size() == 1: compare the top element of MinHeap, regulate the heap.  

**Attention: Do not use java.util.TreeSet in case the duplicates.**  

```java
class MedianFinder {
    PriorityQueue<Integer> small, large;
    /** initialize your data structure here. */
    public MedianFinder() {
        small = new PriorityQueue<>();
        large = new PriorityQueue<>(compare);
    }
    public Comparator<Integer> compare = new Comparator<Integer>(){
    @Override
    public int compare(Integer o1, Integer o2) {
      // TODO Auto-generated method stub
      return (int)(o2 - o1);
    }
    };

    public void addNum(int num) {
        if(large.isEmpty()){
            large.offer(num);
            return ;
        }
        if(small.size() == large.size()){
            if(num < large.peek()){
                large.offer(num);
            }
            else{
                small.offer(num);
            }
        }
        else if(large.size() > small.size()){
            if(num > large.peek()){
                small.offer(num);
            }
            else{
                small.offer(large.poll());
                large.offer(num);
            }
        }
        else if(small.size() > large.size()){
            if(num < small.peek()){
                large.offer(num);
            }
            else{
                large.offer(small.poll());
                small.offer(num);
            }
        }
    }

    public double findMedian() {
        if(small.size() == large.size()){
            return (small.peek() + large.peek()) / 2.0;
        }
        else if(small.size() - large.size() == 1){
            return (double)small.peek();
        }
        else{
            return (double)large.peek();
        }

    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */
```

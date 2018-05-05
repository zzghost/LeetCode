# Implement Stack using Queues
Implement the following operations of a stack using queues.

+ push(x) -- Push element x onto stack.
+ pop() -- Removes the element on top of the stack.
+ top() -- Get the top element.
+ empty() -- Return whether the stack is empty.  

**Notes:**
You must use only standard operations of a queue -- which means only `push to back`, `peek/pop from front`, `size`, and `is empty` operations are valid.  
Depending on your language, queue may not be supported natively. You may simulate a queue by using a list or deque (double-ended queue), as long as you use only standard operations of a queue.  
You may assume that all operations are valid (for example, no pop or top operations will be called on an empty stack).  

## Solution
```java
class MyStack {
    Queue<Integer> queue1, queue2;
    /** Initialize your data structure here. */
    public MyStack() {
        queue1 = new LinkedList<>();
        queue2 = new LinkedList<>();
    }

    /** Push element x onto stack. */
    public void push(int x) {
        queue1.offer(x);
    }

    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        while(queue1.size() != 1){
            queue2.offer(queue1.poll());
        }
        int topElement = queue1.poll();
        Queue tmp = queue1;
        queue1 = queue2;
        queue2 = tmp;
        return topElement;
    }

    /** Get the top element. */
    public int top() {
        while(queue1.size() != 1){
            queue2.offer(queue1.poll());
        }
        int topElement = queue1.peek();
        queue2.offer(queue1.poll());
        Queue tmp = queue1;
        queue1 = queue2;
        queue2 = tmp;
        return topElement;
    }

    /** Returns whether the stack is empty. */
    public boolean empty() {
        return queue1.isEmpty();
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */
```

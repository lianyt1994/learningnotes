在要加元素的时候，先把元素先放到别的地方，再放回来
```java
class MyQueue {

    //一个用来存数据的，一个用来倒腾数据的
    LinkedList<Integer> stack;
    LinkedList<Integer> stack2;
    
    /** Initialize your data structure here. */
    public MyQueue() {
        stack = new LinkedList<>();
        stack2 = new LinkedList<>();
    }
    
    /** Push element x to the back of queue. */
    public void push(int x) { 
            while(!stack2.isEmpty()){
                stack.push(stack2.pop());
            }
            stack.push(x);
            while(!stack.isEmpty()){
                stack2.push(stack.pop());
            }
    }
    
    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
            return stack2.pop();
    }
    
    /** Get the front element. */
    public int peek() {
            return stack2.peek();
    }
    
    /** Returns whether the queue is empty. */
    public boolean empty() {
        return  stack2.isEmpty();
    }
}
```

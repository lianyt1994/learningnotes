双队列
```java
class MyStack {
  //using two queue. The push is inefficient.
  private Queue<Integer> q1 = new LinkedList<Integer>();
  private Queue<Integer> q2 = new LinkedList<Integer>();
  public void push(int x) {
      if(q1.isEmpty()) {
          q1.add(x);
          for(int i = 0; i < q2.size(); i ++)
              q1.add(q2.poll());
      }else {
          q2.add(x);
          for(int i = 0; i < q1.size(); i++)
              q2.add(q1.poll());
      }
  }

  public void pop() {
      if(!q1.isEmpty()) 
          q1.poll();
      else
          q2.poll();
  }
  public int top() {
      return q1.isEmpty() ? q2.peek() : q1.peek();
  }
  public boolean empty() {
      return q1.isEmpty() && q2.isEmpty();
  }
}
```
单队列
```java
class MyStack 
{
    Queue<Integer> queue;
    
    public MyStack()
    {
        this.queue=new LinkedList<Integer>();
    }
    
    // Push element x onto stack.
    public void push(int x) 
    {
       queue.add(x);
       for(int i=0;i<queue.size()-1;i++)
       {
           queue.add(queue.poll());
       }
    }

    // Removes the element on top of the stack.
    public void pop() 
    {
        queue.poll();
    }

    // Get the top element.
    public int top() 
    {
        return queue.peek();
    }

    // Return whether the stack is empty.
    public boolean empty() 
    {
        return queue.isEmpty();
    }
}
```

```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
public class Solution {
    public int minMeetingRooms(Interval[] intervals) {
        Arrays.sort(intervals, new Comparator<Interval>(){
            @Override
            public int compare(Interval i1, Interval i2){
                if(i1.start==i2.start) return i1.end-i2.end;
                else return i1.start-i2.start;
            }
        });
        
        PriorityQueue<Integer> myQ= new PriorityQueue<Integer>();
        int room=0;
        for(Interval interval: intervals){
            myQ.offer(interval.end);
            if(interval.start<myQ.peek()) room++;
            else myQ.poll();
        }
        
        return room;
    }
}

```

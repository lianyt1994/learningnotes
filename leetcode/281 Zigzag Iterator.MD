```java
public class ZigzagIterator {
    private List<List<Integer>> vectors = new ArrayList<>();
    private int row, col;
    private int max;
    public ZigzagIterator(List<Integer> v1, List<Integer> v2) {
        vectors.add(v1);
        vectors.add(v2);
        max = Math.max(v1.size(), v2.size());
    }
 
    public int next() {
        hasNext();
        return vectors.get(row++).get(col);
    }
 
    public boolean hasNext() {
        while (col<max) {
            while (row<vectors.size()) {
                if (col<vectors.get(row).size()) return true;
                row ++;
            }
            row = 0;
            col ++;
        }
        return false;
    }
}
 
/**
 * Your ZigzagIterator object will be instantiated and called as such:
 * ZigzagIterator i = new ZigzagIterator(v1, v2);
 * while (i.hasNext()) v[f()] = i.next();
 */

```

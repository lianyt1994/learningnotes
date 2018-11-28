```java
public class GetFactor {
    public static List<List<Integer>> getFactor(int n) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> out = new ArrayList<>();
        helper(n, 2, out, res);
        return res;
    }
    
    private static void helper(int n, int start, List<Integer> out,
            List<List<Integer>> res) {
        if (n == 1) {
            if (out.size() > 1) {
                res.add(new ArrayList<>(out));
            }
        } else {
            for (int i = start; i <= n; i++) {
                if (n % i == 0) {
                    out.add(i);
                    helper(n / i, i, out, res);
                    out.remove(out.size() - 1);
                }
            }
        }
    }
}

```

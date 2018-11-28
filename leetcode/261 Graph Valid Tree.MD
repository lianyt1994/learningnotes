广度优先
```JAVA
public class Solution {
    public boolean validTree(int n, int[][] edges) {
        Map<Integer, Set<Integer>> graph = new HashMap<>();
        for(int i=0; i<edges.length; i++) {
            for(int j=0; j<2; j++) {
                Set<Integer> pairs = graph.get(edges[i][j]);
                if (pairs == null) {
                    pairs = new HashSet<>();
                    graph.put(edges[i][j], pairs);
                }
                pairs.add(edges[i][1-j]);
            }
        }
        Set<Integer> visited = new HashSet<>();
        Set<Integer> current = new HashSet<>();
        visited.add(0);
        current.add(0);
        while (!current.isEmpty()) {
            Set<Integer> next = new HashSet<>();
            for(Integer node: current) {
                Set<Integer> pairs = graph.get(node);
                if (pairs == null) continue;
                for(Integer pair: pairs) {
                    if (visited.contains(pair)) return false;
                    next.add(pair);
                    visited.add(pair);
                    //可以用移除掉的方法，来保证不会走回去
                    graph.get(pair).remove(node);
                }
            }
            current = next;
        }
        return visited.size() == n;
    }
}

```
深度优先
```JAVA
public class Solution {
    private boolean[] visited;
    private int visits = 0;
    private boolean isTree = true;
    private void check(int prev, int curr, List<Integer>[] graph) {
        if (!isTree) return;
        if (visited[curr]) {
            isTree = false;
            return;
        }
        visited[curr] = true;
        visits ++;
        for(int next: graph[curr]) {
            //也可以把上一个节点也传过去，先判断一下是不是上一个节点
            if (next == prev) continue;
            check(curr, next, graph);
            if (!isTree) return;
        }
        
    }
    public boolean validTree(int n, int[][] edges) {
        visited = new boolean[n];
        List<Integer>[] graph = new List[n];
        for(int i=0; i<n; i++) graph[i] = new ArrayList<>();
        for(int[] edge: edges) {
            graph[edge[0]].add(edge[1]);
            graph[edge[1]].add(edge[0]);
        }
        check(-1, 0, graph);
        return isTree && visits == n;
    }
}

```
并查集的方法
```JAVA
public class Solution {
    public boolean validTree(int n, int[][] edges) {
        if (edges.length != n-1) return false;
        int[] roots = new int[n];
        for(int i=0; i<n; i++) roots[i] = i;
        for(int i=0; i<edges.length; i++) {
            int root1 = root(roots, edges[i][0]);
            int root2 = root(roots, edges[i][1]);
            if (root1 == root2) return false;
            roots[root2] = root1;
        }
        return true;
    }
    private int root(int[] roots, int id) {
        if (id == roots[id]) return id;
        return root(roots, roots[id]);
    }
}

```

```java
public List<Integer> findMinHeightTrees(int n, int[][] edges) {
    if (n == 1) return Collections.singletonList(0);

    List<Set<Integer>> adj = new ArrayList<>(n);
    for (int i = 0; i < n; ++i) adj.add(new HashSet<>());
    for (int[] edge : edges) {
        adj.get(edge[0]).add(edge[1]);
        adj.get(edge[1]).add(edge[0]);
    }

    List<Integer> leaves = new ArrayList<>();
    for (int i = 0; i < n; ++i)
        if (adj.get(i).size() == 1) leaves.add(i);

    while (n > 2) {
        n -= leaves.size();
        //新建一个List专门来存放叶子结点，其实用
        List<Integer> newLeaves = new ArrayList<>();
        for (int i : leaves) {
            int j = adj.get(i).iterator().next();
            //可以用剔除list中的元素，也可以专门放一个数组来--，减到1就放进去
            adj.get(j).remove(i);
            if (adj.get(j).size() == 1) newLeaves.add(j);
        }
        leaves = newLeaves;
    }
    return leaves;
}
```
```java
List<List<Integer>> myGraph = new ArrayList<List<Integer>>();
    List<Integer> res = new ArrayList<Integer>();
    if (n==1) {
      res.add(0);
      return res;
    }
    int[] degree = new int[n];
    for(int i=0; i<n; i++) {
    	myGraph.add(new ArrayList<Integer>());
    }
    for(int i=0; i<edges.length; i++) {
    	myGraph.get(edges[i][0]).add(edges[i][1]);
    	myGraph.get(edges[i][1]).add(edges[i][0]);
    	degree[edges[i][0]]++;
    	degree[edges[i][1]]++;
    }
    Queue<Integer> myQueue = new ArrayDeque<Integer>();
    
    for(int i=0; i<n; i++) 
    	if (degree[i]==0) 
    		return res;
    	else if (degree[i]==1) {
        //把叶子结点放进队列中
    		myQueue.offer(i);
    	}
    
    while (!myQueue.isEmpty()) {
    	res = new ArrayList<Integer>();
    	int count = myQueue.size();
      
    	//根据这个count的个数来剔除queue中的元素
    	for(int i=0; i<count; i++){
    		int curr = myQueue.poll();
    		res.add(curr);
        //把自己减掉
    		degree[curr]--;
    		for(int k=0; k<myGraph.get(curr).size(); k++) {
    			int next = myGraph.get(curr).get(k);
          //为0就是讨论过了，为1就是叶子结点
    			if (degree[next]==0) continue;
          //如果不是0就减1
    			degree[next]--;
          //减1后如果是1就说明是叶子结点
          if (degree[next]==1) {
    				myQueue.offer(next);
    			}
    		}
    	}      	
    }
    return res;
```

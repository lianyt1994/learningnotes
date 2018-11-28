```JAVA
public class WordDistance {
    HashMap<String,ArrayList<Integer>> map = new HashMap<String,ArrayList<Integer>>();
 
    public WordDistance(String[] words) {
        for (int i = 0; i < words.length; i++) {
            if(!map.containsKey(words[i])) {
                map.put(words[i], new ArrayList<Integer>());
            }
            map.get(words[i]).add(i);
        }
    }
 
    public int shortest(String word1, String word2) {
        int shortest = Integer.MAX_VALUE;
        ArrayList<Integer> list1 = map.get(word1);
        ArrayList<Integer> list2 = map.get(word2);
        for (Integer l1:list1) {
            for (Integer l2:list2) {
                shortest = Math.min(shortest, Math.abs(l1 - l2));
            }
        }
        return shortest;
    }
}

```

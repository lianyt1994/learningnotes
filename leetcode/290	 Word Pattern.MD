```java
class Solution {
    public boolean wordPattern(String pattern, String str) {
        String[] ss = str.trim().split(" +");
        if(ss.length!=pattern.length())return false;
        Map<Character,String> map = new HashMap<>();
        for(int i = 0;i<pattern.length();i++){
            String s =  map.get(pattern.charAt(i));
            if(s == null){
                if(map.containsValue(ss[i])){
                    return false;
                }else{
                    map.put(pattern.charAt(i),ss[i]);
                }
            }else if(!s.equals(ss[i])){
                return false;
            }
        }
        return true;
    }
}
```
put方法的返回值： 
1.如果该key已经存放在map中，则返回其映射的旧值； 
2.如果不存在，则返回null，表示没有该key对应的映射（也有可能原来的映射是key-null）
```java
public boolean wordPattern(String pattern, String str) {
    String[] words = str.split(" ");
    if (words.length != pattern.length())
        return false;
    Map index = new HashMap();
    for (Integer i=0; i<words.length; ++i)
        //
        if (index.put(pattern.charAt(i), i) != index.put(words[i], i))
            return false;
    return true;
}
```

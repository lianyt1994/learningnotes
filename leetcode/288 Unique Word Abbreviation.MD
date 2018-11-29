```java
public class ValidWordAbbr {
    HashMap<String, String> set;
    public ValidWordAbbr(String[] dictionary) {
        set = new HashMap<String, String>();
        for(int i = 0 ; i < dictionary.length; i++){
            String temp = dictionary[i];
            if(set.containsKey(getKey(temp)) && !set.get(getKey(temp)).equals(temp))
            //如果有两个以上一样的就改为""，这样判断的时候就一定不一样
                set.put(getKey(temp) , "");
            else
                set.put(getKey(temp) , temp);
            
        }
    }
    
    public String getKey(String s){
        if(s.length() <= 2) return s;
        else{
           return s.charAt(0)+Integer.toString(s.length()-2)+s.charAt(s.length()-1);
        }
    }

    public boolean isUnique(String word) {
        if(set.containsKey(getKey(word))){
            return set.get(getKey(word)).equals(word);
        }
        else
            return true;
    }
}


// Your ValidWordAbbr object will be instantiated and called as such:
// ValidWordAbbr vwa = new ValidWordAbbr(dictionary);
// vwa.isUnique("Word");
// vwa.isUnique("anotherWord");
```

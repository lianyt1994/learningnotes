```java
public class Solution {
    public boolean isOneEditDistance(String s, String t) {
        int len1 = s.length();
        int len2 = t.length();
        if (len1 < len2){
            return isOneEditDistance(t, s);
        }
        if (len1 - len2 > 1){
            return false;
        }
        boolean flag = false;
        if (len1 == len2){
            for (int i = 0; i < len1; i++){
                if (s.charAt(i) != t.charAt(i)){
                    if (!flag){
                        flag = true;
                    } else {
                        return false;
                    }
                }
            }
            return flag;
        } else {
            int sStart = 0;
            int tStart = 0;
            while (tStart < len2){
                if (s.charAt(sStart) == t.charAt(tStart)){
                    tStart++;
                    sStart++;
                } else {
                    if (!flag){
                        flag = true;
                        sStart++;
                    } else {
                        return false;
                    }
                }
            }
            return true;
        }
    }
}
```
```java
public class Solution {
    public boolean isOneEditDistance(String s, String t) {
        for (int i = 0; i < Math.min(s.length(), t.length()); i++){
            if (s.charAt(i) != t.charAt(i)){
                if (s.length() == t.length()){
                    return s.substring(i + 1).equals(t.substring(i + 1));
                } else if (s.length() == t.length() - 1){
                    return s.substring(i).equals(t.substring(i + 1));
                } else {
                    return s.substring(i + 1).equals(t.substring(i));
                }
            }
        }
        return Math.abs(s.length() - t.length()) == 1;
    }
}
```

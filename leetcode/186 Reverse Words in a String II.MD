```java
public class Solution {
    private void reverse(char[] s, int from, int to) {
        while (from<to) {
            char c = s[from];
            s[from] = s[to];
            s[to] = c;
            from ++;
            to --;
        }
    }
    public void reverseWords(char[] s) {
        int pos = 0;
        for(int i=0; i<=s.length; i++) {
            if (i<s.length && s[i] != ' ') continue;
            reverse(s, pos, i-1);
            pos = i+1;
        }
        reverse(s, 0, s.length-1);
    }
}
```

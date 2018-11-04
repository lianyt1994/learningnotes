```java
class Solution {
    public String getHint(String secret, String guess) {
        int[] a= new int[10];
        int[] b= new int[10];
        int count= 0;
        for(int i=0;i<secret.length();i++){
            if(secret.charAt(i)==guess.charAt(i)){
                count++;
            }else{
                a[secret.charAt(i)-'0']++;
                b[guess.charAt(i)-'0']++;
            }
        }
        int count2=0;
        for(int i=0;i<a.length;i++){
            if(a[i]-b[i]>0){
                count2+=b[i];
            }else{
                count2+=a[i];
            }
        }
        return count+"A"+count2+"B";
    }
}
```
```java
public String getHint(String secret, String guess) {
    int bulls = 0;
    int cows = 0;
    int[] numbers = new int[10];
    for (int i = 0; i<secret.length(); i++) {
        if (secret.charAt(i) == guess.charAt(i)) bulls++;
        else {
            //这里是先判断大小再++
            if (numbers[secret.charAt(i)-'0']++ < 0) cows++;
            if (numbers[guess.charAt(i)-'0']-- > 0) cows++;
        }
    }
    return bulls + "A" + cows + "B";
}
```

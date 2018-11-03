```java
class Solution {
    public int addDigits(int num) {
        return (num%9 != 0 || num == 0) ? num%9 : 9;
    }
}
```
```java
class Solution {
    public int addDigits(int num) {
        while(num>9){
            int a=0;
            while(num>0){
                a+=num%10;
                num = num/10;
            }
            num = a;
        }
        return num;
    }
}
```

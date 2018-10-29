Given a positive integer, return its corresponding column title as appear in an Excel sheet.

For example:

    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
    ...
Example 1:

Input: 1
Output: "A"
Example 2:

Input: 28
Output: "AB"
Example 3:

Input: 701
Output: "ZY"

```java
public String convertToTitle(int n) {
      return n == 0 ? "" : convertToTitle(--n / 26) + (char)('A' + (n % 26));
  }
```

```java
public String convertToTitle(int n) {
      StringBuilder sb = new StringBuilder();
      int temp = n-1;
      while(temp >= 0){
         //记得int和char相加得到的是int，要强转
          sb.append((char)((temp)%26+'A'));
          //每次循环之前要先把1减掉
          temp = temp /26-1;
      }
      return sb.reverse().toString();
  }
```

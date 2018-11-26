```JAVA
public static int romanToInt(String s) {
    if (s == null || s.length() == 0)
      return -1;
    HashMap<Character, Integer> map = new HashMap<Character, Integer>();
    map.put('I', 1);
    map.put('V', 5);
    map.put('X', 10);
    map.put('L', 50);
    map.put('C', 100);
    map.put('D', 500);
    map.put('M', 1000);
    int len = s.length(), result = map.get(s.charAt(len - 1));
    for (int i = len - 2; i >= 0; i--) {
      //如果前面比后面小的话，就减去前面的
      if (map.get(s.charAt(i)) >= map.get(s.charAt(i + 1)))
        result += map.get(s.charAt(i));
      else
        result -= map.get(s.charAt(i));
    }
    return result;
}
```
```java
public int romanToInt(String s) {
     int sum=0;
    //出现的话减去两倍
    if(s.indexOf("IV")!=-1){sum-=2;}
    if(s.indexOf("IX")!=-1){sum-=2;}
    if(s.indexOf("XL")!=-1){sum-=20;}
    if(s.indexOf("XC")!=-1){sum-=20;}
    if(s.indexOf("CD")!=-1){sum-=200;}
    if(s.indexOf("CM")!=-1){sum-=200;}
    
    char c[]=s.toCharArray();
    int count=0;
    
   for(;count<=s.length()-1;count++){
       if(c[count]=='M') sum+=1000;
       if(c[count]=='D') sum+=500;
       if(c[count]=='C') sum+=100;
       if(c[count]=='L') sum+=50;
       if(c[count]=='X') sum+=10;
       if(c[count]=='V') sum+=5;
       if(c[count]=='I') sum+=1;
       
   }
   
   return sum;
    
}
```

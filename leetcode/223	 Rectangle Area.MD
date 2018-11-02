求两个长方形的面积之和
<br>就是多了一个判断
```java
public int computeArea(int A, int B, int C, int D, int E, int F, int G, int H) {
        
    int areaOfSqrA = (C-A) * (D-B);
     int areaOfSqrB = (G-E) * (H-F);

    int left = Math.max(A, E);
    int right = Math.min(G, C);
    int bottom = Math.max(F, B);
    int top = Math.min(D, H);

    //If overlap
    int overlap = 0;
    if(right > left && top > bottom)
         overlap = (right - left) * (top - bottom);

    return areaOfSqrA + areaOfSqrB - overlap;
}
```

```java
int computeArea(int A, int B, int C, int D, int E, int F, int G, int H) {
    int left = max(A,E), right = max(min(C,G), left);
    int bottom = max(B,F), top = max(min(D,H), bottom);
    return (C-A)*(D-B) - (right-left)*(top-bottom) + (G-E)*(H-F);
}
```

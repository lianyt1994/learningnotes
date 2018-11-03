记录引用i篇的有几篇，超过L的一定可以，一直往左走就可以了
```java
public int hIndex(int[] citations) {
	int L = citations.length;
	if(L<1) return 0;
	int[] counts = new int[L+1];
	for(int i : citations) {
		if(i>L) counts[L]++;
		else counts[i]++;
	}
	int res = 0;
	for(int k=L; k>=0; k--) {
	    res += counts[k];
	    if(res>=k) return k;
	}
	return 0;
}
```
排序
```java
public class Solution {
    public int hIndex(int[] citations) {
        Arrays.sort(citations);
        int len=citations.length;
        //int count=0;
        int i=len-1;
        for(; i>=0; i--){
            if(citations[i]<(len-i)) break;
        }
        return len-1-i;
    }
}
```

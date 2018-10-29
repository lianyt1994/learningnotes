Compare two version numbers version1 and version2.
If version1 > version2 return 1; if version1 < version2 return -1;otherwise return 0.

You may assume that the version strings are non-empty and contain only digits and the . character.
The . character does not represent a decimal point and is used to separate number sequences.
For instance, 2.5 is not "two and a half" or "half way to version three", it is the fifth second-level revision of the second first-level revision.

Example 1:

Input: version1 = "0.1", version2 = "1.1"
Output: -1
Example 2:

Input: version1 = "1.0.1", version2 = "1"
Output: 1
Example 3:

Input: version1 = "7.5.2.4", version2 = "7.5.3"
Output: -1

```java
class Solution {
    public int compareVersion(String version1, String version2) {
        String[] ver1 = version1.split("\\.");
        String[] ver2 = version2.split("\\.");

        int length1 = ver1.length;
        int length2 = ver2.length;
        int maxLen = Math.max(length1, length2);

        for (int i = 0; i < maxLen; i++) {
            int temp1 = 0, temp2 = 0;
            if (i < length1) {
                temp1 = Integer.parseInt(ver1[i]);
            }
            if (i < length2) {
                temp2 = Integer.parseInt(ver2[i]);
            }
            if (temp1 > temp2) {
                return 1;
            } else if (temp1 < temp2) {
                return -1;
            }
        }
        return 0;

    }
}
```

```JAVA
public class Codec {

    public String encode(List<String> strs) {
        if (strs == null)
            throw new IllegalArgumentException("strs is null");
        StringBuffer buffer = new StringBuffer();
        for (String str : strs) {
            buffer.append(str.length());
            buffer.append(":");
            buffer.append(str);
        }
        return buffer.toString();
    }


    public List<String> decode(String s) {
        List<String> ret = new ArrayList<String> ();
        int next_start = 0;
        while (next_start < s.length()) {
            //从next_start开始的第一位":"的位置
            int split_index = s.indexOf(":", next_start);
            int len = Integer.valueOf(s.substring(next_start, split_index));
            String item = s.substring(split_index+1, split_index+1+len);
            ret.add(item);
            next_start = split_index+1+len;
        }
        return ret;
    }
}

```

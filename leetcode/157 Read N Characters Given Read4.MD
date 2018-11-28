```JAVA
public int read(char[] buf, int n) {
    if(n == 0)
        return 0;
    int read = 0;
    char[] buffer4 = new char[4];
    while(true)
    {
        int r = read4(buffer4);
        for(int i = 0;i<r && read<n;i++)
        {
            buf[read++]= buffer4[i];
        }
        if(r != 4)
            break;
    }
    return read;
}
```

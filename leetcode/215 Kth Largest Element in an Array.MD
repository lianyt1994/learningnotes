```java
public int findKthLargest(int[] nums, int k) 
    {
    	return quickSort(0,nums.length-1,nums,k);        
    }
    
    int quickSort(int low,int high,int[] temp,int k)
    {
    	if(low>=high)return temp[low];//递归结束的约束条件
    	int point=partition(low,high,temp);//每一次分割后“轴”的下标
    	
    	if(temp.length-point==k) return temp[point];
    	else if(temp.length-point>k){
    		return quickSort(point+1,high,temp,k);
    	}
    	else{
    		return quickSort(low,point-1,temp,k);
    	}
    }
    
    public int partition(int low,int high,int[] temp)//采用分治的思想
    {
    	int cur=temp[low];
    	while(low<high)
    	{
        //记得这个等号要加上，不然会陷入死循环
    		while(low<high&&temp[high]>=cur)
    			--high;
    		temp[low]=temp[high];
    		while(low<high&&temp[low]<=cur)
    			++low;
    		temp[high]=temp[low];
    	}
    	temp[low]=cur;
    	return low;
    }


```

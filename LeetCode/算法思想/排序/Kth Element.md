# Kth Element

215. Kth Largest Element in an Array (Medium) 

 [力扣](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/description/) 





### 一：【排序】 

 时间复杂度：O（NlogN） 空间复杂度：O(1)

```java
public int findKthLargest(int[] nums, int k) {
    Arrays.sort(nums);
    return nums[nums.length-k];
}
```

### 二：【堆】   

 时间复杂度：O（NlogK）    空间复杂度：O（K）

```java
public int findKthLargest(int[] nums, int k) {
    PriorityQueue<Integer> pq = new PriorityQueue<>();//小顶堆
    for(int num : nums){
        pq.offer(num);
        if(pq.size() > k){// 维护堆的大小为k
            pq.poll();
        }
    }
    return pq.peek();
}
```

### 三：快速选择

 时间复杂度：O（N） 空间复杂度：O(1)

利用partition可以以O（n）时间复杂度得到数组中任意第K大的数字。

```java
public int findKthLargest(int[] nums, int k) {
    int l = 0;
    int r = nums.length-1;
    k = nums.length-k;
    while(l<r){
        int index = partition(nums,l,r);
        if(index == k){
            return nums[k];
        }else if(index > k){
            r = index-1;
        }else{
            l = index +1;
        }
    }
    return nums[l];
}
public int partition(int[] arr,int l,int r){
    int less = l-1;
    int more = r;
    while(l < more){
        if(arr[l] < arr[r]){
            swap(arr,++less,l++);
        }else if(arr[l] > arr[r]){
            swap(arr,--more,l);
        }else{
            l++;
        }
    }
    swap(arr,l,r);
    return l;
}
public void swap(int[] arr,int i,int j){
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```


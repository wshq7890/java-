# 桶排序-出现频率最多的k个元素

```
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        HashMap<Integer,Integer> map = new HashMap<>();
        for(int num : nums){
            if(map.containsKey(num)){
                int temp = map.get(num);
                temp++;
                map.put(num,temp);
            }else{
                map.put(num,1);
            }
        }
        List<Integer>[] bucket = new List[nums.length];
        for(Integer key : map.keySet()){
            List<Integer> list = bucket[map.get(key)];
            if(list == null){
                list = new ArrayList<>();
            }
            list.add(key);
        }
        List<Integer> res = new ArrayList<>();
        int count = 0;
        for(int i = nums.length-1; i>=0 ; i--){
            if(count == k){
                return res;
            }
            if(bucket[i] != null){
                //把bucket[i]对应的list中的数字加入到res中
                for(Integer num : bucket[i]){
                    res.add(num);
                    count++;
                }
            }else{
                //如果bucket[i]对应的list是空的
                continue;
            }
        }
        return res;                                 
    }
}
```


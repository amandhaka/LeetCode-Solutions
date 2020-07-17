Given a non-empty array of integers, return the k most frequent elements.

Example 1:

Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
Example 2:

Input: nums = [1], k = 1
Output: [1]
Note:

You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
Your algorithm's time complexity must be better than O(n log n), where n is the array's size.
It's guaranteed that the answer is unique, in other words the set of the top k frequent elements is unique.
You can return the answer in any order.

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer,Integer> map=new HashMap<>();
        for(int i=0;i<nums.length;i++) map.put(nums[i],map.getOrDefault(nums[i],0)+1);
        PriorityQueue<Integer> pq=new PriorityQueue<>((a,b)->map.get(b)-map.get(a));
        pq.addAll(map.keySet());
        int[] res=new int[k];
        for(int i=0;i<k;i++)
            res[i]=pq.remove();
        return res;
    }
}
```

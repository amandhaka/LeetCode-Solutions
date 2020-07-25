Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e.,  [0,1,2,4,5,6,7] might become  [4,5,6,7,0,1,2]).

Find the minimum element.

The array may contain duplicates.

Example 1:

Input: [1,3,5]
Output: 1
Example 2:

Input: [2,2,2,0,1]
Output: 0

```java

class Solution {
    public int findMin(int[] nums) {
        if(nums[0]<nums[nums.length-1]) return nums[0];
        int lo=0;
        int hi=nums.length-1;
        while(lo<hi){
            int mid=lo+(hi-lo)/2;
            if(nums[mid]>nums[hi]){
                lo=mid+1; 
            } else if(nums[mid]<nums[hi]){
                hi=mid; //because mid element can be the minimum element here. And in above condition it can't be
                //because we if thea array is not rotated that case is checked already and without that there is 
                //no rotation that will make the lowest on left
            } else{
                //if(nums[mid]==nums[lo]) lo++; 
                    hi--;
            }
        }
        return nums[lo];
    }
}
10 1 10 10 10
```

# 42. Trapping Rain Water
Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.


The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. 
In this case, 6 units of rain water (blue section) are being trapped. Thanks Marcos for contributing this image!
```
Example:
Input: [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

## Solution
```java
/*
A simple approach would be to just make two arrays for left max which will keep track of left maximum
cell height upto ith index and right max will keep track of maximum height upto ith index so just take
minimum of left max and right max at ith index and subtract ith height with that. But this will take o(n) space.
O(1) space solution:
Take two pointers for leftmax and right max and keep leftmax at 1 and rightmax at end of array. leftmax will hold the maximum upto ith index and right max will hold maximum upto jth index. so with each iteration we check if height at ith index and jth index so whichever is lower we know we can fill water in that that cell as we have rightmax in the right and leftmax upto ith index and vice versa.
we can also say that if leftmax<rightmax so water capacity will depend upon leftmax or vice versa.
*/
class Solution {
    public int trap(int[] h) {
        if(h.length<3)
            return 0;
        int water=0;
        int lmax=0;
        int rmax=0;
        int i=0;
        int j=h.length-1;
        while(i<j){
            lmax=Math.max(h[i],lmax);
            rmax=Math.max(h[j],rmax);
            if(h[i]<=h[j]){
                water+=Math.min(lmax,rmax)-h[i];
                i++;
            }
            else{
                water+=Math.min(lmax,rmax)-h[j];
                j--;
            }
        }
        return water;
    }
}
```

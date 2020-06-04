# Longest Substring Without Repeating Characters
Given a string, find the length of the longest substring without repeating characters.
```
Example 1:

Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3. 
Example 2:

Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
Example 3:

Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if(s.length()==0 || s==null){
            return 0;
        }
        Set<Character> set=new HashSet<>();
        int left=0;
        int right=0;
        int max=0;
        while(right<s.length()){
            if(set.add(s.charAt(right))){
                right++;
                max=Math.max(max,right-left);
            }
            else{
                set.remove(s.charAt(left));
                left++;
            }
        }
        return max;       
    }
}
```

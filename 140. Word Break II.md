Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, add spaces in s to construct a sentence where each word is a valid dictionary word. Return all such possible sentences.

Note:

The same word in the dictionary may be reused multiple times in the segmentation.
You may assume the dictionary does not contain duplicate words.
Example 1:
```
Input:
s = "catsanddog"
wordDict = ["cat", "cats", "and", "sand", "dog"]
Output:
[
  "cats and dog",
  "cat sand dog"
]
```
Example 2:
```
Input:
s = "pineapplepenapple"
wordDict = ["apple", "pen", "applepen", "pine", "pineapple"]
Output:
[
  "pine apple pen apple",
  "pineapple pen apple",
  "pine applepen apple"
]

Explanation: Note that you are allowed to reuse a dictionary word.
```
Example 3:
```
Input:
s = "catsandog"
wordDict = ["cats", "dog", "sand", "and", "cat"]
Output:
[]
```
```java

class Solution {
    public List<String> wordBreak(String s, List<String> wordDict) {
        return wordHelper(s,wordDict,new HashMap<>());
    }
    public List<String> wordHelper(String s,List<String> wordDict,Map<String,List<String>> map){
        if(map.containsKey(s)){
            return map.get(s);
        }      
        List<String> res=new ArrayList<>();
        if(s.length()==0){
            res.add("");
            return res;
        }
        for(String word:wordDict){
            if(s.startsWith(word)){
                String subString=s.substring(word.length());
                List<String> subList=wordHelper(subString,wordDict,map);
                for(String curr:subList){
                    String optionalSpace=curr.isEmpty()?"":" ";
                    res.add(word+optionalSpace+curr);
                    //System.out.println(word+" " + res+" -> "+curr);
                }
            }
            //System.out.println(res);
        }
        map.put(s,res);
        System.out.println(map);
        return res;
    }
}
```

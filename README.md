# Group Anagrams
## https://leetcode.com/problems/group-anagrams

Given an array of strings, group anagrams together.
```
Example:

Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```
**Note:**
1. All inputs will be in lowercase.
2. The order of your output does not matter.

# Implementation :
```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        List<List<String>> groupedAnagrams = new ArrayList<>();
        if(strs == null || strs.length == 0)
            return groupedAnagrams;
        
        Map<String,List<String>> map = new HashMap<>();
        for(String s : strs) {
            char[] ch = s.toCharArray();
            Arrays.sort(ch);
            String sorted = new String(ch);
            if(!map.containsKey(sorted)) {
                map.put(sorted, new ArrayList<>());
            }
            map.get(sorted).add(s);
        }
        groupedAnagrams.addAll(map.values());
        return groupedAnagrams;
    }
}
```

# References :
https://www.youtube.com/watch?v=ptgykfAEax8

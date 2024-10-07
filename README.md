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

# Implementation 1 : Naive Approach (Checking each string if it is an anagram of any of previous strings)
```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        List<List<String>> result = new ArrayList<>();
        if(strs == null || strs.length == 0)
          return result;
        Map<String, List<String>> map = new HashMap<>();
        List<String> first = new ArrayList<>();
        first.add(strs[0]);
        map.put(strs[0], first);
        for(int i = 1; i < strs.length; i++) {
            String str = strs[i];
            boolean isAnagram = false;
            Set<String> keys = map.keySet();
            for(String key : keys) {
                if(isAnagram(key, str)) {
                    map.get(key).add(str);
                    isAnagram = true;
                    break;
                }
            }
            if(!isAnagram){
                List<String> list = new ArrayList<>();
                list.add(str);
                map.put(str, list);
            }
        }
        for(String key : map.keySet()){
            result.add(map.get(key));
        }
        return result;
    }

    private boolean isAnagram(String s1, String s2) {
        if(s1.length() != s2.length())
          return false;
        Map<Character,Integer> freq = new HashMap<>();
        for(char ch : s1.toCharArray()) {
            int count = freq.getOrDefault(ch, 0);
            freq.put(ch, count + 1);
        }  
        for(int i = 0; i < s2.length(); i++) {
            char ch = s2.charAt(i);
            if(!freq.containsKey(ch))
              return false;
            int count = freq.get(ch);
            if(count < 1)
              return false;
            freq.put(ch, count - 1);    
        }
        return true;
    }
}
```

# Implementation 2 : While Checking first sort the current string and just check if it is already in the Map
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

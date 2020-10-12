[link](https://leetcode.com/problems/remove-duplicate-letters/)  

1.  First loop the string to count the occurence of each letter [O(n)]  
2. loop again the given string
  if current letter is not used and is smaller than the previous letters `pre` we push bask in the string and there are more letter `pre` in the following letters in the string   then pop letter `pre` and push back current letter [O(n)]  
 
Input: s = "cbacdcbc"  
Output: "acdb"
```cpp
class Solution {
public:
    string removeDuplicateLetters(string s) {
        vector<int> vec(26,0);
        vector<int> use(26,0);
        string ans;
        for(auto a:s) vec[a-'a']++;
       
        for(auto a:s)
        {
            vec[a-'a']--;
            if(use[a-'a']++) continue;
            while(!ans.empty() && vec[ans.back()-'a']>0 && ans.back()>a)
            {
                char t=ans.back();
                ans.pop_back();
                use[t-'a']=0;
            }
            ans+=a;
        }
            
        return ans;
            
         
        }
};
```

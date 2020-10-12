[link](https://leetcode.com/problems/two-sum/)
## Brute Force
It needs to enumerate all set of i,j which i!=j and i,j is index of nums  
Time Complexity O(n)  
## One pass with hash table
The basic idea is we can loop only once by storing the difference between target and current element in hash table.  
If current element is in the hash table, it means there is an element adding up with current element equals target.
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int,int> map;
        for(int i=0;i<nums.size();i++)
        {
            if(map.find(nums[i])!=map.end()) return {map[nums[i]],i};
            else    map[target-nums[i]]=i;
        }
        return {};
    }
};
```

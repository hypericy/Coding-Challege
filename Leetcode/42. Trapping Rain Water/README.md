[link](https://leetcode.com/problems/trapping-rain-water/)
# DP
The idea is every point can trap water if there are right and left bars taller than its height.  
And the amount of the water trapped at `i` is the minimum height between the tallest bar by its left and the tallest one by its right minus its height.  
```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        if(height.size()==0) return 0;
        int *dp = new int[height.size()];
        int max_back = height[height.size()-1];
        int ans=0;
        dp[0]=height[0];
        for(int i=1;i<height.size();i++)
        {
            dp[i] = max(height[i],dp[i-1]);
        }
            
        for(int i=height.size()-2;i>=0;i--)
        {
            max_back = max(max_back,height[i]);
            if(min(dp[i],max_back) - height[i]>0) ans+=min(dp[i],max_back) - height[i];
        }
        return ans;   
    }
};
```
# two pointer
The idea is similar to DP, but this time we don't need to iterate the vector first. We use two pointer start from the leftmost and rightmost index.
Each time we choose the lower bar between the two pointer to move forward and set its height as water level if it is higher than the previous level.
If it's not then we can trap water by the difference between previous level and this lower bar.   
```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        //if(height.size()==0) return 0;
        int l=0,r=height.size()-1,level=0;
        int ans=0,low_bound;
        while(l<r)
        {
            low_bound = height[l]<height[r]?height[l++]:height[r--];
            level = max(level,low_bound);
            ans+=level-low_bound;
        }
        return ans;   
    }
};
```

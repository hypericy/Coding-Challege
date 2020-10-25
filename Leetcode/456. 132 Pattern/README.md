[link](https://leetcode.com/problems/132-pattern/)
# Stack
The idea is looping through the numbers from the beginning first and record the minimum number so far in an array. O(n)  
Then loop from the back to find 3 and 2.  
So we push every number which is bigger than the minimum number we stored previously to a stack.  
Beacuse if nums[i] equals min[i] it means there is no bigger number in the front , it can't be selected as 3 or 2.  
Then we pop up stack if the top of stack is smaller than current min,therefore top of stack can be a candidate of 2.  
If nums[i]>stack.top return true

  means 3 and 2
Example [1,2,3,4]  
min=[1,1,1,1]
1. 4 stack=[4]  
2. 3 stack=[4,3]  
3. 2 stack=[4,3,2]  
4. 1 stack=[4,3,2,1]  
False  

Example [3,1,4,2]  
min=[3,1,1,1]  
1. 2 stack[2]  
2. 4 stack[2]  
[1,4,2] found  
True  

Example [6,12,3,4,6,11,20]  
min=[6,6,3,3,3,3,3]  
1. 20 stack=[20]  
2. 11 stack=[20,11]  
3. 6 stack=[20,11,6]  
4. 4 stack=[20,11,6,4]    
5. 3 pass(euals min)  
6. 12 stack=[20,11,12] pop 6,4 (<=min)  
```cpp
class Solution {
public:
    bool find132pattern(vector<int>& nums) {
        vector<int> vec(nums.size());
        stack<int> st;
        vec[0]=nums[0];
        for(int i=1;i<nums.size();i++)
            vec[i]=min(nums[i],vec[i-1]);
        for(int i=nums.size()-1;i>=0;i--)
        {
            if(nums[i]!=vec[i]){
                while(!st.empty() && st.top()<=vec[i])
                    st.pop();
                if(!st.empty() && st.top()<nums[i])
                    return true;
                st.push(nums[i]);
            }
        }
        return false;
    }
};
```

[link](https://leetcode.com/problems/create-sorted-array-through-instructions/)
# Binary Search finding low Bound and up Bound
```cpp
class Solution {
public:
    int binarySearch(vector<int> &sort,int num)
    {
        int size = sort.size();
        int upBound,lowBound;
        if(size==0){
            sort.push_back(num);
            return 0;
        }
        int l=0,r=size-1,m;
        while(l<=r)
        {
            m=(l+r)/2;
            if(sort[m]<=num){
                l = m+1;
            }
            else{
                r= m-1;
            }
        }
        upBound = l;
        l=0,r=size-1;
        while(l<=r)
        {
            m=(l+r)/2;
            if(sort[m]<num){
                l = m+1;
            }
            else{
                r= m-1;
            }
        }
        lowBound = r+1;
        sort.insert(sort.begin()+upBound,num);
        
        return min(lowBound,size-upBound);
    }
    int createSortedArray(vector<int>& instructions) {
        int ans=0;
        vector<int> sort;
        for(int i:instructions)
        {
            ans += binarySearch(sort,i);
        }
        return ans;
    }
};
```

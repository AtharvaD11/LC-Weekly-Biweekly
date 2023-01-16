Problem Link : https://leetcode.com/contest/weekly-contest-328/problems/count-the-number-of-good-subarrays/

Solution : 


Variation of 'count number of substrings having atleast k distinct charachters'

Link : https://github.com/AtharvaD11/Two-Pointers/blob/main/SET%20B/03.%20CountNumberOfSubstringsHavingAtLeastKDistinctCharacters.md

Code :


```
class Solution {
public:
    long long countGood(vector<int>& nums, int k) {
        long long pairs = 0;
        int start = 0;
        int end = 0;
        int n = nums.size();
        map<int,int> mp;
        long long ans = 0;
        while(start < n && end < n){
            if(mp.find(nums[end]) != mp.end()){
                pairs += mp[nums[end]];
                mp[nums[end]]++;
                
            }
            else{
                mp[nums[end]]++;
                
            }
            if(pairs >= k){
                ans += (n - end);
            }
            while(pairs >= k){
                mp[nums[start]]--;
                pairs -= mp[nums[start]];
                if(mp[nums[start]] == 0) mp.erase(nums[start]);
                if(pairs >= k){
                    ans += (n-end);
                }
                start++;
            }
            
            end++;
        }
        return ans;
    }
};
// TC : O(n)

```

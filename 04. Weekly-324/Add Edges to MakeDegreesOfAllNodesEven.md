Problem Link : https://leetcode.com/contest/weekly-contest-324/problems/add-edges-to-make-degrees-of-all-nodes-even/

Solution :

Intuition<br>
The number of odd degree node must be even: 0,2,4,...
if odd.size() == 0, return True
if odd.size() == 2, TODO
if odd.size() == 4, TODO
if odd.size() > 4, return false


Explanation<br>
find the mapping G where G[i] is the neighbour set of node i.
Find out the list of nodes with odd degree.

In case if we have 2 odds:
option1:
we can link them together,
if they are not neighbour.

option2:
we can link both them to node i,
if node i is not neighbour of either of them.

otherwise return false.

In case if we have 4 odds a,b,c,d
option1: We can link (a,b) and (c,d)
option2: We can link (a,c) and (b,d)
option3: We can link (a,d) and (c,b)
otherwise return false.


```
class Solution {
public:
    bool isPossible(int n, vector<vector<int>>& edges) {
        vector<int> degree(n+1, 0);
        map<pair<int,int>, bool> mp;
        for(auto V : edges){
            int u = V[0];
            int v = V[1];
            degree[u]++;
            degree[v]++;
            mp[{u,v}] = true;
            mp[{v,u}] = true;
        }
        vector<int> odd;
        for(int i=1;i<=n;i++){
            if(degree[i]&1){
                odd.push_back(i);
            }
        }
        if(odd.size() == 0) return true;
        else if(odd.size() == 2){
            int a = odd[0];
            int b = odd[1];
            if(mp[{a,b}] == 0) return true;
            for(int i=1;i<=n;i++){
                if(i == a || i == b) continue;
                if(mp[{a,i}] == 0 && mp[{b,i}] == 0) return true;
            }
            return false;
        }
        else if(odd.size() == 4){
            int a = odd[0];
            int b = odd[1];
            int c = odd[2];
            int d = odd[3];
        
            if(mp[{a,b}] == 0 && mp[{c,d}] == 0) return true;
            if(mp[{a,c}] == 0 && mp[{b,d}] == 0) return true;
            if(mp[{a,d}] == 0 && mp[{c,b}] == 0) return true;
            return false;
        }
        else return false;
    }
};



```
1) TC : O(n)<br>
2) SC : O(n)
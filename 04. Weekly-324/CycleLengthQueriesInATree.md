Problem Link :  https://leetcode.com/contest/weekly-contest-324/problems/cycle-length-queries-in-a-tree/

Solution : 

Since the tree follows a familiar pattern we don't have to make the tree. We find the common ancestor of the two nodes and then we add the distances from that node to get the answer.

```
class Solution {
public:
    vector<int> rootToNode(int n){
        vector<int> res;
        while(n){
            res.push_back(n);
            n = n/2;
        }
        return res;
    }
    
    int lca(int a, int b){
        vector<int> path1 = rootToNode(a);
        vector<int> path2 = rootToNode(b);
        for(int i=0;i<path1.size();i++){
            for(int j=0;j<path2.size();j++){
                if(path1[i] == path2[j]){
                    return i + j + 1;
                }
            }
        }
        return -1;
    }
    
    vector<int> cycleLengthQueries(int n, vector<vector<int>>& queries) {
        vector<int> ans;
        for(auto i : queries){
            ans.push_back(lca(i[0], i[1]));
        }
        return ans;
    }
};
```

1) TC : O(n^2)
2) SC : O(n)
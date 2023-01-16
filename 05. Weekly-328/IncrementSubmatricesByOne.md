Problem Link : https://leetcode.com/problems/increment-submatrices-by-one/

Solution : 
Difference array variation for 2d arrays


Code : 

```
class Solution {
public:
    vector<vector<int>> rangeAddQueries(int n, vector<vector<int>>& queries) {
        vector<vector<int>> mat(n, vector<int>(n, 0));
        for(auto &v : queries){
            int r1 = v[0];
            int c1 = v[1];
            int r2 = v[2];
            int c2 = v[3];
            
            mat[r1][c1]++;
            if(c2 + 1 < n)mat[r1][c2 + 1] --;
            if(r2 + 1 < n)mat[r2+1][c1] --;
            if(r2 + 1 < n && c2 + 1 < n)mat[r2 + 1][c2 + 1] ++;
            
        }
        
        for(int i=0;i<n;i++){
            for(int j=1;j<n;j++){
                mat[i][j] += mat[i][j-1];
            }
        }
        for(int i=1;i<n;i++){
            for(int j=0;j<n;j++){
                mat[i][j] += mat[i-1][j];
            }
        }
        return mat;
    }
};

// TC : O(n*n)
```
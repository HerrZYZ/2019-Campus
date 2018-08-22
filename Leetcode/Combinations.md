#### 1. 找出[1, 2, ..., n]中所有长为k的组合数
```cpp
class Solution {
public:
    //有向图：结点i有指向i+1,i+2,...,n的路径， i=1,2,...,n
    //找出所有长为k的路径
    vector<vector<int>> combine(int n, int k) {
        vector<int> path;
        vector<vector<int> > paths;
        find_all_paths(0,k,n,path,paths);
        return paths;
    }
    void find_all_paths(int i, int need_len, int& n, vector<int>& path, vector<vector<int> >& paths) {
        if (need_len == 0) {
            paths.push_back(path);
            return;
        }
        for (int j = i+1; j <= n; j++) {
            path.push_back(j);
            find_all_paths(j, need_len-1, n, path, paths);
            path.pop_back();
        }
    }
};
```

[Path Sum II](https://leetcode.com/problems/path-sum-ii/description/)

Solution 1:
```cpp
class Solution {
public:
    vector<vector<int>> pathSum(TreeNode* root, int sum) {
        vector<vector<int> > paths;
        vector<int> path;
        if (!root) return paths;
        path.push_back(root->val);
        _path_sum(root,sum-root->val,path,paths);
        return paths;
    }
    void _path_sum(TreeNode* root, int sum, vector<int>& path, vector<vector<int> >& paths) {
        if(!root->left && !root->right) {
            //leaf sum should = 0
            if (sum == 0) {
                paths.push_back(path);
            } 
        } else {
            // not leaf, sum should > 0 // wrong, target sum can be negative
            // if (sum > 0) {
                int val;
                if (root->left) {
                    val = root->left->val;
                    path.push_back(val);
                    _path_sum(root->left, sum - val, path, paths);
                    path.pop_back();
                }
                if (root->right) {
                    val = root->right->val;
                    path.push_back(val);
                    _path_sum(root->right, sum - val, path, paths);
                    path.pop_back();                
                }
            // } 
        }
    }
};
```
Solution 2:
```cpp
class Solution {
public:
    vector<vector<int>> pathSum(TreeNode* root, int sum) {
        vector<vector<int> > paths;
        if (!root) return paths;
        vector<int> path;
        _path_sum(root,sum,path,paths);
        return paths;
    }
    void _path_sum(TreeNode* root, int sum, vector<int>& path, vector<vector<int> >& paths) {
        sum -= root->val;
        path.push_back(root->val);
        if(!root->left && !root->right) { //is leaf
            if (sum == 0) {
                paths.push_back(path);
            } 
        } else {
            if (root->left) {
                _path_sum(root->left, sum, path, paths);
            }
            if (root->right) {
                _path_sum(root->right, sum, path, paths);
            }
        }
        path.pop_back();
    }
};
```

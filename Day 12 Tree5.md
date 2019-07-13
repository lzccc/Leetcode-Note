# Day 12

## Tree

### P662

```c++
/**
 * 使用给树的成员编坐标的思想解体。
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int widthOfBinaryTree(TreeNode* root) {
        int result = 0;
        if(!root) return result;
        if(root->left == NULL && root->right == NULL) return 1;
        map<float, vector<float>> mp;
        vector<float> vt;
        findWidth(0.0, 0.0, root, mp, result);
        return result+1;
    }
    void findWidth(float x, float y, TreeNode* & root, map<float, vector<float>> &mp, int & result){
        if(!root) return;
        if(mp.find(y) != mp.end()){
            if(x < mp[y][0]) mp[y][0] = x;
            else if(x > mp[y][1]) mp[y][1] = x;
        }else{
            vector<float> vt(2, x);
            mp[y] = vt;
            if(x < mp[y][0]) mp[y][0] = x;
            else if(x > mp[y][1]) mp[y][1] = x;
        }
        float tmp = mp[y][1] - mp[y][0];
        if(tmp > result) result = int(tmp);
        if(root->left) findWidth(x+x, y+1, root->left, mp, result); //关键！！
        if(root->right) findWidth(x+x+1, y+1, root->right, mp, result); //关键！！
    }
};
```

### P103

```c++
/**
 * 可以使用两个stack来解题，一个装从左到右的，一个装从右到左的。
 * 我这边直接使用reverse了。。。
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int>> result;
        if(root == nullptr) return result;
        queue<TreeNode*> q;
        q.push(root);
        int check = 0;
        while(1){
            int size = q.size();
            if(size == 0) break;     
            vector<int> temp_res;
            while(size --){
                TreeNode* temp = q.front();
                q.pop();
                temp_res.push_back(temp->val);
                if(temp->left != nullptr)
                    q.push(temp->left);                    
                if(temp->right != nullptr)
                    q.push(temp->right);
            }
            if(check == 1){
                reverse(temp_res.begin(), temp_res.end());
                check = 0;
            }            
            else if(check == 0){
                check = 1;
            }
            result.push_back(temp_res);    
            temp_res.resize(0);
        }
        return result;
    }
};
```

### P113

```c++
class Solution {
public:
    vector<vector<int>> pathSum(TreeNode* root, int sum) {
        vector<vector<int>> result;
        vector<int> vec;
        if(!root) return result;
        sumPath(root, sum, result, vec);
        return result;
    }
    void sumPath(TreeNode* root, int num, vector<vector<int>> & result, vector<int> vec){
        if(!root) return ;
        vec.push_back(root->val);
        if(root->val == num && root->left == NULL && root->right == NULL){
            result.push_back(vec);
        } 
        else {
            if(root->left) sumPath(root->left, num-root->val, result, vec);
            if(root->right) sumPath(root->right, num-root->val, result, vec);
        }
        
    }
};
```


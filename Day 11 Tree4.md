# Day 11

## Tree

### P450

```c++
/**
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
    TreeNode* deleteNode(TreeNode* root, int key) {
        if(!root)
            return NULL;
        TreeNode* node = root, *parent = NULL;
        while(node){
            if(node->val == key)
                break;
            if(node->val < key){
                parent = node;
                node = node->right;
            }else{
                parent = node;
                node = node->left;
            }
        }
        if(!node)
            return root;
        else if(!parent){
            return delRoot(root);
        }else if(parent->left == node){
            parent->left = delRoot(node);
        }else{
            parent->right = delRoot(node);
        }
        return root;
    }
    TreeNode* delRoot(TreeNode* root){
        if(!root)
            return NULL;
        else if(!root->left && !root->right)
            return NULL;
        else if(!root->left){
            return root->right;
        }
        else if(!root->right){
            return root->left;
        }else{
            TreeNode* parent = root;
            TreeNode* node = root->right;
            while(node->left){
                parent = node;
                node = node->left;
            }
            swap(root->val, node->val);
            if(parent->right == node){
                parent->right = node->right;
            }else{
                parent->left = node->right;
            }
            return root;
        }        
    }
};
```

### P102

```c++
/**
 * 使用两层while循环的方法很常见，注意使用
 */
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> result;
        if(root == nullptr) return result;
        queue<TreeNode*> q;
        q.push(root);
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
            result.push_back(temp_res);    
            temp_res.resize(0);
        }
        return result;
    }
};
```

### P987

```c++
class Solution {
public:
    struct newStr{        
        int val;
        int height;
    };
    static bool cmp1(newStr* a, newStr* b)//先按x从小到大排，相同，再按y从小到大
    { 
        return a->height < b->height || (a->height == b->height) && (a->val < b->val);
    }
    vector<vector<int>> verticalTraversal(TreeNode* root) {
        vector<vector<int>> result;
        if(root == nullptr) return result;
        //queue<TreeNode*> q;
        map<int, vector<newStr*>> mp;
        mapAdd(0, 0, mp, root);
        while(mp.size()>0){
            vector<int> temp1;
            vector<newStr*> temp2 = mp.begin()->second;
            sort(temp2.begin(), temp2.end(), cmp1);
            while(temp2.size() > 0){
                temp1.push_back(temp2[0]->val);
                temp2.erase(temp2.begin());
            }
            result.push_back(temp1);
            mp.erase(mp.begin());
        }
        return result;
    }
    void mapAdd(int s, int k, map<int, vector<newStr*>> &mp, TreeNode* & root){           
                TreeNode* temp = root;
                std::map<int, vector<newStr*>>::iterator it;
                it = mp.find(s);
                if(it == mp.end()){
                    vector<newStr*> temp_res;
                    newStr* tempStr = new newStr();;
                    tempStr->val = temp->val;
                    tempStr->height = k;
                    temp_res.push_back(tempStr);
                    mp[s] = temp_res;
                }else{
                    newStr* tempStr = new newStr();
                    tempStr->val = temp->val;
                    tempStr->height = k;
                    mp[s].push_back(tempStr);
                } 
                if(temp->left != nullptr)
                    mapAdd(s-1, k+1, mp, temp->left) ;              
                if(temp->right != nullptr)
                    mapAdd(s+1, k+1, mp, temp->right) ;                 
    }
};
```


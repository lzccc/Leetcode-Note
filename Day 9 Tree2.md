# Day 9

## Tree

### P872

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
/**
 * 注意如果left和right声明在函数体之外，则程序用时将大大增加，可能是
 * 因为更改堆中和栈中的数据结构耗时不同所致。
 */
class Solution {
public:
    bool leafSimilar(TreeNode* root1, TreeNode* root2) {
        vector<int> left;
        vector<int> right;
        leafValue(root1, left);
        leafValue(root2, right);
        return left == right;
    }
    void leafValue(TreeNode* root, vector<int> &sequence){
        if(root == NULL) return;
        if(root->left == NULL && root->right == NULL) sequence.push_back(root->val);
        leafValue(root->left, sequence);
        leafValue(root->right, sequence);
    }
};
```

### P94

```c++
/**
 * 技巧是使用两层while循环代替递归。
 */
class Solution {
private:
    vector<int> inorder;
    stack<TreeNode *> stak;
public:
    vector<int> inorderTraversal(TreeNode* root) {
        if(root == NULL) return inorder;
        stak.push(root);
        while(stak.empty() != true){
            while(root){
                root = root->left;
                if(root) stak.push(root);
            }

            inorder.push_back(stak.top()->val);
            TreeNode * tmp = stak.top();
            root = tmp->right;
            stak.pop();
            if(root) stak.push(root);
        }
        return inorder;
    }
};
```

### P897

```c++
/**
 * 创建新node会影响空间复杂度，直接更改tree较为复杂，但是空间复杂度为O(1)
 */
class Solution {
    TreeNode* newroot = new TreeNode(0);
    TreeNode* curr = newroot;
public:
    TreeNode* increasingBST(TreeNode* root) {
        if (root == NULL) return NULL;
        increasingBST(root->left);
        curr->right = new TreeNode(root->val);
        curr = curr->right;
        increasingBST(root->right);
        return newroot->right;
    }
};
```


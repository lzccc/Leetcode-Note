# Day 8

## Tree

### P104

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
    int maxDepth(TreeNode* root) {
        if(root == NULL) return 0;
        if(root->left == NULL && root->right == NULL) return 1;
        int left = maxDepth(root->left);
        int right = maxDepth(root->right);
        int depth = (left > right)? left : right;
        depth++;
        return depth;
    }
};
```

### P110

```c++
class Solution {
public:
    bool balance = true;
    bool isBalanced(TreeNode* root) {
        if(root == NULL) return true;
        if(root->left == NULL && root->right == NULL) return 1;
        maxDepth(root);
        if(balance) return true;
        return false;
    }
    int maxDepth(TreeNode* root) {
        if(root == NULL) return 0;
        if(root->left == NULL && root->right == NULL) return 1;
        int left = maxDepth(root->left);
        int right = maxDepth(root->right);
        if(abs(left - right) > 1) balance = false;
        int depth = max(left, right);
        depth++;
        return depth;
    }
};
```

### P543

```c++
class Solution {
private:
    int num = 0;
public:
    int diameterOfBinaryTree(TreeNode* root) {
        if(!root) return 0;
        maxDepth(root);
        return num-1;
    }
    
    int maxDepth(TreeNode* root) {
        if(root == NULL) return 0;
        if(root->left == NULL && root->right == NULL){
            int tmp2 = 1;
            if(tmp2 > num) num = tmp2;
            return 1;
        } 
        int left = maxDepth(root->left);
        int right = maxDepth(root->right);
        int tmp = left + right + 1;
        if(tmp > num) num = tmp;
        int depth = (left > right)? left : right;
        depth++;
        return depth;
    }
};
```




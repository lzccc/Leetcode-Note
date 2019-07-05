# Day 10

## Tree

### P105

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
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        return blt(preorder, inorder, 0, preorder.size()-1, 0, inorder.size()-1);
    }

    TreeNode* blt(vector<int>& preorder, vector<int>& inorder, int pstart, int pend, int istart, int iend){
        if(pstart>pend || istart> iend) return NULL;
        int val = preorder[pstart];
        int i = istart;
        while(inorder[i]!=val) i++;
        TreeNode* root = new TreeNode(val);
        root->left = blt(preorder, inorder, pstart+1, pstart+i-istart, istart, i-1);
        root->right = blt(preorder, inorder, pend-(iend-i)+1, pend, i+1, iend);
        return root;
    }
};
```

### P951

```c++
class Solution {
    bool result = true;
public:
    bool flipEquiv(TreeNode* root1, TreeNode* root2) {
        if(root1 == NULL && root2 == NULL) return true;
        if(root1 == NULL || root2 == NULL) return false;
        if(root1->val != root2->val) return false;
        int aleft = 0, aright=0, bleft = 0, bright = 0;
        if(root1->left) aleft = root1->left->val;
        if(root1->right) aright = root1->right->val;
        if(root2->left) bleft = root2->left->val;
        if(root2->right) bright = root2->right->val;

        if(aleft == bleft && aright == bright){
            flipEquiv(root1->left, root2->left);
            flipEquiv(root1->right, root2->right);
        }else if(aleft == bright && aright == bleft){
            flipEquiv(root1->left, root2->right);
            flipEquiv(root1->right, root2->left);
        }else{
            result = false;
        }
        return result;
    }
};
```


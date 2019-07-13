# Day 13

## Tree

### P22

```c++
/**
 * 简单的递归
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
    int countNodes(TreeNode* root) {
        int result = 0;
        if(!root) return 0;
        if(!root->left && !root->right) return 1;
        return 1 + countNodes(root->left) + countNodes(root->right);
    }
};
```

### P236

```c++
/**
 * 这题要找两个节点最近的一个公共父节点，构造两个栈，用递归的方法找每个节点构成的树
 * 中能不能发现要找的节点，发现了就压入栈中，结果就是最后压入的节点都是两个的父节点
 * 然后我们逐一剔除栈顶的相同元素，因为这些父节点不是最近的，最后发现最后一个相同的
 * 公共节点便是答案。
 */
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        TreeNode* ancestor = root;
        stack<TreeNode*> stc1;
        stack<TreeNode*> stc2;
        findNode(root, p, stc1);
        findNode(root, q, stc2);
        while((stc1.size() > 0 && stc2.size() > 0) && stc1.top()->val == stc2.top()->val){
            ancestor = stc1.top();
            stc1.pop();
            stc2.pop();
        }
        return ancestor;
    }
    bool findNode(TreeNode* root, TreeNode* target, stack<TreeNode*> &stc){
        if(!root) return false;
        if(root->val == target->val){
            stc.push(root);
            return true;
        } 
        bool leftFind = findNode(root->left, target, stc);
        bool rightFind = findNode(root->right, target, stc);
        bool find = leftFind || rightFind;
        if(find) stc.push(root);
        return find;
    }   
};
```

### P113

```c++
/**
 * 需要找到这两个节点，就要用inorder的顺序从小到大逐一查找是否有逆序对，最后调换第一个逆序对
 * 的前面的元素和最后一个逆序对的后一个元素得到答案。
 * eg: 1 [9] 3 4 5 6 7 8 [2]
 */
class Solution {
public:
    void traverse(TreeNode* root, TreeNode* &prev, TreeNode* &first, TreeNode* &second) {
    if (!root) return;
    traverse(root->left, prev, first, second);
    // found that the order is reversed
    if (prev && prev->val > root->val) {
        if (first) second = root;
        else  {first = prev; second = root;}
    }
    prev = root;
    traverse(root->right, prev, first, second);
}
    void recoverTree(TreeNode* root) {
        TreeNode *first = nullptr, *prev = nullptr, *second = nullptr;
        traverse(root, prev, first, second);
        // swap
        if (first && second) {
            int tmp = first->val;
            first->val = second->val;
            second->val = tmp;
        }
    }
};
```


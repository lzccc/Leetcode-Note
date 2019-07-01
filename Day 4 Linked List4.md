# Day4

## Linked List

### P160

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        unordered_set<ListNode*> nodes;
        while (headA) {
            nodes.insert(headA);
            headA = headA -> next;
        }
        while (headB && nodes.find(headB) == nodes.end()) {
            headB = headB -> next;
        }
        return headB;
    }
};
```

### P142

```c++
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        unordered_set<ListNode *> nodes;
        while(head){
            nodes.insert(head);
            if(nodes.find(head->next) != nodes.end()) return head->next;
            head = head->next;
        }
        return NULL;
    }
};
```

### P21

```c++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(l1 == NULL) return l2;
        if(l2 == NULL) return l1;
        ListNode* curr1=l1, * curr2=l2, * next1=nullptr, * next2=nullptr, *last1 = nullptr, *last2 = nullptr;
        while(curr1 && curr2){
            if(curr1->val <= curr2->val){
                last2 = NULL;
                next1 = curr1->next;
                curr1->next = curr2;
                if(last1) last1->next = curr1;
                last1 = curr1;
                curr1 = next1;
            }else{
                last1 = NULL;
                next2 = curr2->next;
                curr2->next = curr1;
                if(last2) last2->next = curr2;
                last2 = curr2;
                curr2 = next2;
            }
        }
        return (l1->val <= l2->val) ? l1 : l2;
    }
};
```


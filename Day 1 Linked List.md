# Day 1
## Linked List
### P237
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
    void deleteNode(ListNode* node) {
        node -> val = (node -> next) -> val;
        node -> next = (node -> next) -> next;
    }
};
```

### P203
```c++
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        if(head == NULL){
            return head;
        }
        ListNode* prev = nullptr, *curr = head;
        while(curr){
            if(curr->val == val){
                if(curr == head){
                    head = head->next;
                }else{
                    prev->next = curr->next;
                }
            }else{
                prev = curr;
            }
            curr = curr->next;
        }
     return head;
    }
};
```

### P83
```c++
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode* prevnode = nullptr, *curr = head;
        while(curr){
            if(prevnode == NULL){
                prevnode = curr;
                curr = curr->next;
                continue;
            }
            if(curr -> val == prevnode->val){
                prevnode->next = curr->next;
            }else{
                prevnode = curr;
            }
            curr = curr->next;
        }
        return head;
    }
};
```
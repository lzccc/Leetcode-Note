# Day 2

## Linked List 2

### P19

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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        int position = 0;
        ListNode* waitRemove = nullptr, * curr = head, *last = nullptr;
        while(curr){
            if(position + 1 == n){
                waitRemove = head;
            }
            if(position + 1 > n){
                last = waitRemove;
                waitRemove = waitRemove->next;
            }
            curr = curr->next;
            position++;
        }
        if(waitRemove == head){
            head = head->next;
        }else{
            last->next =  waitRemove->next;
        }
        return head;
    }
};
```

### P206

```c++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* curr = head, * last = nullptr, * nextNode = nullptr;
        while(curr){
            nextNode = curr->next;
            curr->next = last;
            last = curr;
            curr = nextNode;
        }
        return last;
    }
};
```

### P234

```c++
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        ListNode* slow = head, *fast = head;
        ListNode* newhead = nullptr;
        if(head == NULL || head->next == NULL) return true;
        while(fast->next != NULL && fast->next->next != NULL){
            fast = fast->next->next;
            slow = slow->next;
        }
        newhead = slow->next;
        ListNode* last = nullptr, *curr = newhead, *next = nullptr;
        while(curr){
            next = curr->next;
            curr->next = last;
            last = curr;
            curr = next;
        }
        while(last){
            if(last->val != head->val) return false;
            last = last->next;
            head = head->next;
        }
        return true;
    }
};
```


# Day3

## Linked List

### P876

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
    ListNode* middleNode(ListNode* head) {
        ListNode* slow = head, * fast = head;
        while(fast != NULL && fast->next != NULL){
            fast = fast->next->next;
            slow = slow->next;
        }
        return slow;
    }
};
```

### P24

```c++
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if(head == NULL) return head;
        ListNode* newhead = head->next;
        if(head->next == NULL) return head;
        ListNode* curr = head, * nextNode = nullptr, * last = nullptr;
        while(curr != NULL && curr->next != NULL){
            if(last != NULL){
                if(curr->next != NULL) last->next = curr->next;
            } 
            nextNode = curr->next->next; //nextNode == 3
            curr->next->next = curr; //2->1
            curr->next = NULL;
            last = curr; //last == 1
            curr = nextNode; //curr == 3
        }
        if(curr != NULL) last->next = curr;
        return newhead;
    }
};
```

### P143

```c++
class Solution {
public:
    void reorderList(ListNode* head) {
        ListNode* slow = head, *fast = head;
        ListNode* newhead = nullptr;
        if(head == NULL || head->next == NULL) return ;
        while(fast->next != NULL && fast->next->next != NULL){
            fast = fast->next->next;
            slow = slow->next;
        }
        newhead = slow;
        ListNode* last = nullptr, *curr = newhead, *next = nullptr;
        while(curr){
            next = curr->next;
            curr->next = last;
            last = curr;
            curr = next;
        }
        ListNode* currLeft = head, * currRight = last, *leftNext = nullptr, * rightNext = nullptr;
        while(last && head){
            leftNext = head->next;
            rightNext = last->next;
            head->next = last;
            if(last->next) last->next = leftNext;
            head = leftNext;
            last = rightNext;
        }

    }
};
```


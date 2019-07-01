# Day 6

## Linked List

### P92

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
    ListNode* reverseBetween(ListNode* head, int m, int n) {
        int currNum = 1;
        ListNode* firstNode = nullptr, *tailNode = nullptr, * leftNode = nullptr, * rightNode = nullptr,  * lastNode = nullptr, *nextNode = nullptr, * curr = head;
        while(currNum < m){
            if(currNum == m-1) firstNode = curr;
            curr = curr->next;
            currNum += 1;
        }
        leftNode = curr;
        while(currNum <= n){
            nextNode = curr->next;
            curr->next = lastNode;
            lastNode = curr;
            curr = nextNode;
            currNum += 1;
            if(currNum == n) {
                if(firstNode){
                    firstNode->next = curr;
                } else{
                    head = curr;
                }              
            }
        }        
        leftNode->next = curr;
        return head;
    }
};
```

### P25

```c++
class Solution {
public:
    ListNode* reverseKGroup(ListNode* head, int k) {
        if(!head) return head;
        int currNum = 1;
        ListNode *firstNode = head, * lastNode = nullptr, *curr = head, * nextNode = nullptr;
        if(k ==1) return head;

        while(curr){
            if(currNum % k == 1) firstNode = curr;
            curr = curr->next;
            currNum += 1;
            if(currNum % k == 0){
                if(curr) head = reverseBetween(head, currNum-k+1, currNum);
                curr = firstNode;
            } 
        }
        //head = reverseBetween(head, 1, 3);
        return head;
    }

    ListNode* reverseBetween(ListNode* head, int m, int n) {
        int currNum = 1;
        ListNode* firstNode = nullptr, *tailNode = nullptr, * leftNode = nullptr, * rightNode = nullptr,  *                 lastNode = nullptr, *nextNode = nullptr, * curr = head;
        while(currNum < m){
            if(currNum == m-1) firstNode = curr;
            curr = curr->next;
            currNum += 1;
        }
        leftNode = curr;
        while(currNum <= n){
            nextNode = curr->next;
            curr->next = lastNode;
            lastNode = curr;
            curr = nextNode;
            currNum += 1;
            if(currNum == n) {
                if(firstNode){
                    firstNode->next = curr;
                } else{
                    head = curr;
                }              
            }
        }        
        leftNode->next = curr;
        return head;
    }
    
};
```


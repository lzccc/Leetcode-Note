# Day5

## Linked List

### P148

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
    ListNode* sortList(ListNode* head) {
        if(!head || head->next == NULL) return head;
        ListNode* slow = head, * fast = head, * lastSlow = nullptr, *leftHead = nullptr, * rightHead = nullptr;
        while(fast && fast->next){
            fast = fast->next->next;
            lastSlow = slow;
            slow = slow->next;
        }
        lastSlow->next = NULL;
        leftHead = sortList(head);
        rightHead = sortList(slow);
        if(leftHead == NULL) return rightHead;
        if(rightHead == NULL) return leftHead;
        ListNode* curr1=leftHead, * curr2=rightHead, * next1=nullptr, * next2=nullptr, *last1 = nullptr, *last2 = nullptr;
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
        return (leftHead->val <= rightHead->val) ? leftHead : rightHead;
    }
};
```

### P2

```c++
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2){ 
        ListNode result(-1);
        ListNode * curr = &result;
        int carry = 0;
        while(l1 != NULL || l2 != NULL){
            int x = (l1 != NULL) ? l1 -> val : 0;
            int y = (l2 != NULL) ? l2 -> val : 0;
            int sum = x + y + carry;
            carry = sum/10;
            curr -> next = new ListNode(sum % 10);
            curr = curr -> next;
            if(l1) l1 = l1 -> next;
            if(l2) l2 = l2 -> next;
        }
        if(carry) curr -> next = new ListNode(1);
        return result.next;            
    }
};
```

### P445

```c++
class Solution {
    ListNode* newList = new ListNode(-1);
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {

        int carry = 0;
        ListNode *curr1 = l1, *curr2 = l2, *longHead = nullptr;
        int whichList = 1;
        while(curr1 && curr2){
            curr1 = curr1->next;
            curr2 = curr2->next;
        }
        if(curr1){
            whichList = 1;
            longHead = l1;
            while(curr1){
                curr1 = curr1->next;
                longHead = longHead->next;
            }
        }else if(curr2){
            whichList = 2;
            longHead = l2;
            while(curr2){
                curr2 = curr2->next;
                longHead = longHead->next;
            }
        }else{longHead = l1;}
        
        
        newList->next = l1;
        if(whichList == 1){
            while(l2){
                longHead->val = longHead->val + l2->val;
                longHead = longHead->next;
                l2=l2->next;
            }
            newList->next = l1;
        }else{
            while(l1){
                longHead->val = longHead->val + l1->val;
                longHead = longHead->next;
                l1=l1->next;
            }
            newList->next = l2;
        }
        ListNode *result = newList;
        ListNode *curr = result;
        stack<ListNode *> st;
        while(curr){
            st.push(curr);
            curr = curr->next; 
        }
        
        while(!st.empty()){
            st.top()->val += carry;
            if(st.top()->val >=10){
                st.top()->val -= 10;
                carry = 1;
            }else{carry = 0;}
            st.pop();
        }
        if(result->val == 0) result->val += 1;
        if(result->val == -1) return result->next;
        return result;
    }
};
```


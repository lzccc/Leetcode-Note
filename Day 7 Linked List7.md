# Day 7

## Linked List

### P61

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
    ListNode* rotateRight(ListNode* head, int k) {
        if(!head || head->next == NULL) return head;
        stack<ListNode *> st;
        ListNode * curr = head;
        int total = 0;
        int move = 0;
        while(curr){
            st.push(curr);
            total += 1;
            curr = curr->next;
        }
        move = k % total;
        for(int i=0; i<move; i++){
            st.top()->next = head;
            head = st.top();
            st.pop();
            st.top()->next = NULL;
        }
        return head;
    }
};
```

### P146

```c++
struct mycache
{
	int key;
	int value;
	mycache(int x, int y):key(x), value(y){}
};
class LRUCache{    
    unordered_map<int, list<mycache>::iterator> mymap;
    list<mycache> LRUlist;
    int cap;
public:
    LRUCache(int capacity) {
        cap=capacity;
    }

    int get(int key) {
        if(mymap.find(key)==mymap.end()) return -1;
        moveTohead(key);
        return mymap[key]->value;
    }

    void put(int key, int value) {
        if(mymap.find(key)==mymap.end()){
            mycache current(key, value);
            if(LRUlist.size() >= cap){
                mymap.erase(LRUlist.back().key);
                LRUlist.pop_back();
            }
            LRUlist.push_front(current);
            mymap[key] = LRUlist.begin();
            return;       
        }
        mymap[key]->value = value;
        moveTohead(key);
    }
private:
    void moveTohead(int key) 
    {
         mycache newone(key, mymap[key]->value);
         LRUlist.erase(mymap[key]);
         LRUlist.push_front(newone);
         mymap[key] = LRUlist.begin();
    }
};
```

### P706

```c++
class MyHashMap {
public:
    /** Initialize your data structure here. */
    MyHashMap(): container(32, nullptr), len(32)  {
    }
    
    /** value will always be non-negative. */
    void put(int key, int value) {
        int key_ = getKey(key);
        ListNode* cur = container[key_];
        if(!cur)
            container[key_] = new ListNode(key, value);
        else {
            for(; cur; cur = cur->next) {
                if(cur->key == key) {
                    cur->val = value;
                    return;
                }
            }
            ListNode* tmp = new ListNode(key, value);
            tmp->next = container[key_];
            container[key_] = tmp;
        }
    }
    
    /** Returns the value to which the specified key is mapped, or -1 if this map contains no mapping for the key */
    int get(int key) {
        int key_ = getKey(key);
        if(!container[key_]) return -1;
        ListNode* cur = container[key_];
        while(cur && cur->key!= key) cur = cur->next;
        if(!cur) return -1;
        return cur->val;
    }
    
    /** Removes the mapping of the specified value key if this map contains a mapping for the key */
    void remove(int key) {
        int key_ = getKey(key);
        ListNode* pp = container[key_];
        ListNode* last = nullptr;
        while(pp) {            
            if(pp->key != key){
                last = pp;
                pp = pp->next;
            }                
            else {
                if(pp == container[key_]){
                    container[key_] = container[key_]->next;
                    return;
                }                
                if(last) last->next = pp->next;
                delete pp;
                return;
            }
        }
    }
private:
    struct ListNode {
        int key;
        int val;
        ListNode* next;
        ListNode(int _key, int _val): key(_key), val(_val), next(nullptr) {
        }
    };
    int len;
    vector<ListNode* > container;
    int getKey(int key)  {
        return key % len ;
    }
};
```


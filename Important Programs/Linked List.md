[143. Reorder List](https://leetcode.com/problems/reorder-list/)
Intuition -   so its mixing of three problems first we need to find the middle and cut it from the head and the reverse the middle alone , finally merge both the head and reversed middle.
```cpp
/**

 * Definition for singly-linked list.

 * struct ListNode {

 *     int val;

 *     ListNode *next;

 *     ListNode() : val(0), next(nullptr) {}

 *     ListNode(int x) : val(x), next(nullptr) {}

 *     ListNode(int x, ListNode *next) : val(x), next(next) {}

 * };

 */

class Solution {

public:

    ListNode* reverse(ListNode* head){

        ListNode* prev = nullptr;

        ListNode* curr = head;

        ListNode* next = nullptr;

        while(curr!=nullptr){

            next = curr->next;

            curr->next = prev;

            prev = curr;

            curr = next;

        }

        return prev;  

    }

    ListNode* middlefind(ListNode* head){

        ListNode* fast = head;

        ListNode* slow = head;

        ListNode* prev = nullptr;

        while(fast!=nullptr && fast->next!=nullptr){

            prev = slow;

            slow = slow->next;

            fast = fast->next->next;

        }

        if(prev!=nullptr) prev->next = nullptr;

        return slow;

    }

    void reorderList(ListNode* head) {

        if(head==nullptr || head->next==nullptr) return;

        ListNode* middle = middlefind(head);

        middle = reverse(middle);

        ListNode* curr = head;

        ListNode* next;

        ListNode* mnext;

        while(curr!=nullptr && middle!=nullptr){

            next =  curr->next;

            mnext = middle->next;

            curr->next = middle;

            if (next == nullptr) break;

            middle->next = next;

            curr = next;

            middle = mnext;

        }

        }

};
```
[138. Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/)
Intuition  - Here we have to create copy of node which have an another pointer which is set to a random , so first we have to create a new node of the node value and store it in the index of the nodes in the original list.  create an another loop to mark the next and random of the loops in the map.
```cpp
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/

class Solution {
public:
    Node* copyRandomList(Node* head) {
        map<Node*,Node*> mpp;
        Node* temp = head;
        while(temp!=nullptr){
            Node* newnode = new Node(temp->val);
            mpp[temp]=newnode;
            temp=temp->next;
        }
        temp = head;
        while(temp!=nullptr){
            Node* copy = mpp[temp];
            copy->next = mpp[temp->next];
            copy->random = mpp[temp->random];
            temp=temp->next;
        }
        return mpp[head];
    }
};
```
[2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)
Intuition -  Simple math it is in the reverse order so we just have to add each node values together and carry forward the carry and add that to the sum.
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
     ListNode* dummy  =  new ListNode(0);
     ListNode* ans = dummy;
     int carry =0;
     while(l1!=nullptr || l2!=nullptr || carry!=0){
        int x = (l1!=nullptr)?l1->val:0;
        int y = (l2!=nullptr)?l2->val:0;
        int sum = carry+x+y;
        carry = sum/10;
        ans->next = new ListNode(sum%10);
        if(l1!=nullptr){
            l1=l1->next;
        }
         if(l2!=nullptr){
            l2=l2->next;
        }
        ans=ans->next;
     }
     return dummy->next;   
    }
};
```
[141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)
Intuition -  Have two fast and slow pointer move one by 1 and one by 2, if they met it is true that cycle is detected return true.
```cpp
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
    bool hasCycle(ListNode *head) {
    ListNode* slow = head;
    ListNode* fast = head;
    if(head==nullptr) return false;
    while(fast!=nullptr && fast->next!=nullptr){
        slow=slow->next;
        fast=fast->next->next;
        if(slow==fast) return true;
    }
    return false;
    }
};
```
[23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)
#minheap
Intuition -  So here its simple we just have to use minheap in priority queue and store it in that and create a new linked list by popping it adding it to the list.
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        priority_queue<int, vector<int>, greater<int>> pq;
        for(ListNode* list:lists){
            while(list!=nullptr){
                pq.push(list->val);
                list=list->next;
            }
        }
        ListNode* dummy = new ListNode(0);
        ListNode* ans = dummy;
        while(!pq.empty()){
            ans->next  = new ListNode(pq.top());
            pq.pop();
            ans=ans->next;
        }
        return dummy->next;
    }
};
```

[25. Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/)
Intuition -  Here we are reversing by a range from head to tail, doing it repeatedly until tail becomes null with in the range of k so we return head. The reverse function will return reversed from head to tail(tail is excluded) now the head after the reverse function call ends it points to the last node in the reversed list so we point its next to  `recursion(tail,k)`.
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* reverse(ListNode* head,ListNode* tail){
        ListNode* prev= nullptr;
        ListNode* curr= head;
        ListNode* next = nullptr;
        while(curr!=tail){
            next=curr->next;
            curr->next=prev;
            prev=curr;
            curr=next;
        }
        return prev;
    }
    ListNode* reverseKGroup(ListNode* head, int k) {
        if(head==nullptr) return nullptr;
        ListNode* tail = head;
        for(int i=0;i<k;i++){
            if(tail==nullptr){
                return head;
            }
            tail=tail->next;
        }
        ListNode* reversed = reverse(head,tail);
        head->next = reverseKGroup(tail,k);
        return reversed;
    }
};
```


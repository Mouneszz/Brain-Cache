[146. LRU Cache](https://leetcode.com/problems/lru-cache/)
#design #doublylinkedlist
Intuition : Here it is bit hard to think of our own to solve this but  we want to keep in head that we a have to use a doubly linked list , first we have to create  map which stores key and value as a node in that node it will have the key and value. 
- `get` method : check if we have the element in the map if not than `return -1` ,if it is than we have to make that as the most recently use cache so first remove  it from the node and insert it at the head, return the value.
- `put` method :
    - if the element is already present than make that element as the most recently used cache by removing it and inserting it at the head. 
    - else check if the map size reached the capacity if it is than remove the least recently used cache from the map and the node by using the tail, after that add the new node to the map by the key and insert it at the head.
```cpp
class LRUCache {
public:
    class Node{
        public:
        int key;
        int val;
        Node* next;
        Node* prev;
        Node(int key,int val){
            this->key=key;
            this->val=val;
        }
    };
    int capacity;
    Node* head;
    Node* tail;
    unordered_map<int,Node*> mpp;
    LRUCache(int capacity) {
        this->capacity  = capacity;
        head = new Node(0,0); // to act as a dummy head
        tail = new Node(0,0); // to act as a dummy tail
        head->next = tail;
        tail->prev = head;
    }
    
    int get(int key) {
        if(!mpp.count(key)){
            return -1;
        }
        Node* node = mpp[key];
        remove(node);
        insertathead(node);
        return node->val;
    }
    
    void put(int key, int value) {
        if(mpp.count(key)){
            Node* node = mpp[key];
            node->val = value;
            remove(node);
            insertathead(node);
        }
        else{
            if(mpp.size()==capacity){
                mpp.erase(tail->prev->key); //because tail is dummy remove its prev
                remove(tail->prev); // same as above
            }
            Node* node = new Node(key,value);
            mpp[key] = node;
            insertathead(node);
        }
        
    }
    void remove(Node* node){
        node->prev->next = node->next;
        node->next->prev = node->prev;
    }
    void insertathead(Node* node){
        node->next = head->next;
        node->next->prev = node;
        head->next = node;
        node->prev = head;
    }
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```
[2349. Design a Number Container System](https://leetcode.com/problems/design-a-number-container-system/)
Intuition : Here we just create two maps one for the index = number and one for adding all the index inside priority queue in the number `map<int ,priority_queue<int>`. the change  is simple just have to look up if it not present in the first map add an entry into both maps . And for the find we have to return smallest  index which have the number  so we pop our priority queue is now a minheap because of this syntax change `priority_quueu<int,vector<int>,greater<int>>>`.
so we pop until we get a index which have the number in the first map which is minimum in the queue.
```cpp
class NumberContainers {
    unordered_map<int,int> m;
    unordered_map<int,priority_queue<int,vector<int>,greater<int>>> d;
public:
    NumberContainers() {
        
    }
    
    void change(int index, int number) {
        if(m.count(index) && m[index]==number) return;
        m[index]=number;
        d[number].push(index);
    }
    
    int find(int number) {
        if(!d.count(number)) return -1;
        auto &pq = d[number];
        while(!pq.empty() && m[pq.top()]!=number) pq.pop();
        return pq.empty()?-1:pq.top();
    }
};
```
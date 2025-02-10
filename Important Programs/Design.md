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
[208. Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/)
#trie 
Intuition: First we have to create a `TrieNode` which have array of 26 `TreiNode*` which store its  next characters. and also we should declare a `isword` variable to mark is this word finished ,we make it as true in insert function . search and start with is similar compared to but in search we return if the `isword` is true but in starts with we simply return  true after the loop.
```cpp
class TrieNode{
public:
    TrieNode* child[26];
    bool isword;
    TrieNode(){
        isword = false;
        for(int i=0;i<26;i++){
            child[i] = nullptr;
        }
    }
};
class Trie {
public:
    TrieNode* root;
    Trie() {
        root = new TrieNode();
    }
    
    void insert(string word) {
        TrieNode* curr = root;
        for(char &ch:word){
            if(curr->child[ch-'a']==nullptr)
            curr->child[ch-'a'] = new TrieNode();
            curr = curr->child[ch-'a'];
        }
        curr->isword = true;
    }
    
    bool search(string word) {
        TrieNode* curr = root;
        for(char &ch:word){
            if(curr->child[ch-'a']==nullptr) return false;
            curr = curr->child[ch-'a'];
        }
        return curr->isword;
    }
    
    bool startsWith(string prefix) {
        TrieNode* curr = root;
        for(char &ch:prefix){
            if(curr->child[ch-'a']==nullptr) return false;
            curr = curr->child[ch-'a'];
        }
        return true;
    }
};
```
[211. Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure/)
#true
Intuition : So its same as the previous one but we want to include backtracking in it so the insertion is same as above but and also here we used map instead of an array, if we found dot we check all of its children using recursion if its is not return true than it means its is not possible so return false. and if the character is not found inside the map and its not a dot than also return false.
```cpp
class TrieNode{
public:
    unordered_map<char,TrieNode*> child;
    bool isword = false;
    TrieNode(){

    }
};
class WordDictionary {
public:
    TrieNode* root;
    WordDictionary() {
        root = new TrieNode();
    }
    
    void addWord(string word) {
      TrieNode* curr = root;
      for(char& ch:word){
        if(!curr->child.count(ch)){
            curr->child[ch] = new TrieNode();
        }
        curr = curr->child[ch];
      }
      curr->isword = true;  
    }
    bool searchnode(string word,TrieNode* node){
        for(int i=0;i<word.size();i++){
            char ch = word[i];
            if(!node->child.count(ch)){
                if(ch =='.'){
                    for(auto& m:node->child){
                        TrieNode* chil = m.second;
                        if(searchnode(word.substr(i+1),chil)){
                            return true;
                        }
                    }
                    return false; 
                }
                return false;
            }
            else{
                node = node->child[ch];
            }
        }
        return node->isword;
    }
    bool search(string word) {
        return searchnode(word,root);
    }
};
```
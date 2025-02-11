 Tries  are similar to trees but they have map inside the nodes so we can access the child nodes by traversing the map and by that words can be built.
 ```cpp
 class Trienode{
    public:
    unordered_map<char,Trienode*> mpp;
    bool isend; // this is to specify if it is the last letter of the word
    Trienode(){
        isend = false;
    }
};
class Trie{
  public:
  Trienode* root;
  Trie(){
      root = new Trienode();
  }
  void insert(string& word){
      Trienode* curr = root;
      for(char& ch:word){
          if(!curr->mpp.count(ch)){
              curr->mpp[ch] = new Trienode();
          }
          curr=curr->mpp[ch];
      }
      curr->isend = true;
  }
  bool search(string& word){
      Trienode* curr  = root;
      for(char& ch:word){
          if(!curr->mpp.count(ch)) return false;
          curr=curr->mpp[ch];
      }
      return curr->isend;
  }
};
```


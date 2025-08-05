Parenthesis  checker 
```cpp
class Solution {
  public:
    bool isBalanced(string& k) {
        stack<char> st;
        for(char& ch : k){
            if(ch == '}' || ch == ']' || ch == ')'){
                if(st.empty()) return false;
                if((ch == '}' && st.top() != '{') ||
                   (ch == ']' && st.top() != '[') ||
                   (ch == ')' && st.top() != '(')) {
                    return false;
                }
                st.pop();
            } else {
                st.push(ch);
            }
        }
        return st.empty();
    }
};
```

postfix to prefix
```cpp
// User function Template for C++

class Solution {
  public:
    string postToPre(string post_exp) {
        // Write your code here
        stack<string> st;
        string str = post_exp;
        for(int i=0;i<str.size();i++){
            if(str[i]=='*'|| str[i]=='+' || str[i]=='-' || str[i]=='/'){
                string op1  = st.top();
                st.pop();
                string op2 = st.top();
                st.pop();
                
                string temp = string(1,str[i])+op2+op1;
                st.push(temp);
            }
            else{
                st.push(string(1,str[i]));
            }
        }
        
        string ans="";
        while(!st.empty()){
            ans+=st.top();
            st.pop();
        }
        return ans;
    }
};
```

creating queue  with two stacks
```cpp
// User function Template for C++

class Queue {
    stack<int> input, output;
  public:
    void enqueue(int x) {
        while(!input.empty()){
            output.push(input.top());
            input.pop();
        }
        input.push(x);
        while(!output.empty()){
            input.push(output.top());
            output.pop();
        }
    }
    
    int dequeue() {
        if(input.empty()){
            return -1;
        }
        // code here
        int ans = input.top();
        input.pop();
        return ans;
    }
};
```

Stack using two queues
```cpp
class stack{
	queue<int> q1,q2;
	public:
	void push(int x){
	q2.push(x);
	while(!q1.empty()){
		q2.push(q1.front());
		q1.pop();
	}
	swap(q1,q2);
	}
	void pop(){
	if(q1.empty()) return -1;
	q1.pop();
	}
	int top(){
		if(q1.empty()){
		
		}
	}
}
```
[150. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)
```cpp
class Solution {

public:

    int evalRPN(vector<string>& tokens) {

        stack<int> st;

        for(string ch:tokens){

            if(ch=="+"){

                int second = st.top(); st.pop();

                int first = st.top(); st.pop();

                st.push(first + second);

            }

            else if(ch=="-"){

                int second = st.top(); st.pop();

                int first = st.top(); st.pop();

                st.push(first - second);

            }

            else if(ch=="*"){

                int second = st.top(); st.pop();

                int first = st.top(); st.pop();

                st.push(first * second);

            }

            else if(ch =="/"){

                int second = st.top(); st.pop();

                int first = st.top(); st.pop();

                st.push(first / second);

            }

            else{

                st.push(stoi(ch));

            }

        }

        return st.top();

    }

};
```
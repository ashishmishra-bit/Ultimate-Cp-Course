These are also avalible as a PDF [here](https://github.com/uzair-ali10/Ultimate-Cp-Course/blob/main/Phase%20-%20II/Stack%20and%20Queue/Stacks/Stacks.pdf)
# Stacks

## What is Stack?

Stack is an linear data structure in which operations are performed in a particular manner.

operations are performed on `(LIFO) Last in first out` or `(FILO) First in Last out` manner

A new data element is stored by pushing it on the top of the stack. And an data element is retrieved by popping the top element off the stack and returning it.

A stack can be implemented using array as well as linked list but using a linked list is more efficient due to its dynamic nature.

Stacks provides 4 basic operations for interaction

1. `push()` - Adds data to the top of stack
2. `pop()` - Returns and removes data from the top of stack
3. `top()` - Returns data from top of stack (Without removing it)
4. `isEmpty()` - Checks if a stack is empty or not (Return's a Boolean Value)

![Stacks%2037c3d732008d4f00ad1048eb26387644/geek-stack-1.png](Stacks%2037c3d732008d4f00ad1048eb26387644/geek-stack-1.png)

![Stacks%2037c3d732008d4f00ad1048eb26387644/stack-operations.jpg](Stacks%2037c3d732008d4f00ad1048eb26387644/stack-operations.jpg)

In the above image, although item 2 was kept last, it was removed first. This is exactly how the LIFO (Last In First Out) Principle works.

## Why & When Stack?

A Stack data structure is  useful when order of action is important. A stack ensures that system does not move to new action before completing those before it.

Some real-life usage of stack are listed below

1. Reversing: By Default a stack will revere its input as it follows first in last out principle
2. Undo/Redo: This approach can be used in editors to implement the undo and redo functionality. The state of program can be push into a stack each time a change is made. In order to undo use pop() to return and remove the last  change.
3. Recursion: Recursive functions use something called "Call Stack". When a program calls a recursive function that function goes on top of the stack.
4. Call Stack: Programming languages use a data stack to execute code. When a function is called, it is added to the call-stack and removed once completed.
5. In Browser: The back-button in browser saves all the URL you visit in a stack. Each time you visit a new page its URL gets added to top of stack. And when u press back button it is removed and returned from the stack using the `pop()` function.

[Pros and Cons of Stack](https://www.notion.so/b05ddd6bb6394c35a74a6b6029e9837d)

## Working of a Stack

1. A variable called `top` is used to keep track of index at top.
2. On initializing a stack we set value of `top` to -1, and we can also check if stack is empty or not by comparing `nextIndex == -1`.
3. On pushing a new element we place the new element in the position pointed by `top` and increase value of `top`.
4. On popping top element we return the value of element pointed by `top` and then decrease value of `top` .
5. Before pushing we check if stack is already full.
6. before popping we check if stack is already empty.

[Time-Complexity](https://www.notion.so/0e7993e29cb44f01b992d8cccfc67e44)

## Code Implementation

- Stack Using Array

```cpp
#include <iostream>

using namespace std;

#define n 100

class stack{
    int* arr;   //arr and top are private data members.
    int top;

    public:
    stack(){
        arr = new int[n];   //dynamically allocating n size for the array/stack
        top = -1;
    }
    //push
    void push(int x){
        if(top==n-1){
            cout<<"Stack Overflow"<<endl;
            return;
        }
        top++; 
        arr[top] = x;
    }
    //pop
    void pop(){
        if(top==-1){
            cout<<"Stack underflow"<<endl;
            return;
        }
        top--;
    }
    //top
    int Top(){
        if(top==-1){
            cout<<"Empty Stack"<<endl;
            return -1;
        }
        return arr[top];
    }
    //empty
    bool empty(){
        return top==-1;
    }
};

int main(){
    
    stack st;
    st.push(1);
    st.push(2);
    st.push(3);

    cout<<st.Top()<<endl;
    st.pop();
    cout<<st.Top()<<endl;
    st.pop();
    st.pop();
    st.pop();

    cout<<st.empty()<<endl;

    return 0;
}
```

- Stack Using Linked-List

```cpp
#include <iostream>

using namespace std;

class node{
    public:
    int data;
    node* next;
    node(int x){
        data = x;
        next = NULL;
    }
};

class stack{
    node* top;
    
    public:
    stack(){
        top = NULL;
    }

    void push(int x){
        node* n = new node(x);

        n->next = top;
        top = n;
    }

    void pop(){
        if(top==NULL){
            cout<<"Stack Underflow\n";
            return;
        }

        node* todelete = top;
        top = top->next;
        delete todelete;
    }

    int Top(){
        if(top==NULL){
            cout<<"Empty Stack\n";
            return -1;
        }
        return top->data;
    }

    bool empty(){
        return top==NULL;
    }
};

int main(){
    stack st;

    st.push(1);
    st.push(2);
    st.push(3);

    cout<<st.Top()<<endl;
    st.pop();

    cout<<st.Top()<<endl;
    st.pop();

    cout<<st.Top()<<endl;
    st.pop();

    cout<<st.Top()<<endl;
    st.pop();

    cout<<st.empty()<<endl;

    return 0;
}
```

## Using The Inbuilt Stack Data-Structure in STL

Syntax: `stack <data_type> stack_name;`

### Some functions of stack

- `push()` Insert an element at the top of stack `O(1)`
- `pop()` removes a element from the top of stack `O(1)`
- `top()` Acess the top element of the stack `O(1)`
- `empty()` Returns whether the stack is empty or not `O(1)`
- `size()` Returns size of stack `O(1)`

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
	stack <int> stack_name; // Declare a stack

	for (int i = 0; i < 5; i++) { //This loop takes input and adds it to stack
		int temp;
		cin >> temp;
		stack_name.push(temp);
	}

//This loop prints the element of stack and clears the stack at the ending of loop
	while (!stack_name.empty()) { 
		cout << stack_name.top() << " ";
		stack_name.pop();
	}

	return 0;
}
```

## Some Standard Questions:

### Valid Parentheses

[Valid Parentheses - LeetCode](https://leetcode.com/problems/valid-parentheses/)

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

### Approach:

1. Iterate over the input string
2. if the `iTH` element of string is opening bracket then `push()` it
3. else it is a closing bracket, then check if the top of stack contains corresponding opening bracket. 
4. if yes then `pop()`  or else return false.
5. In the end check if stack is empty is yes then return true

```cpp
bool isValid(string s)
{
   stack <char> sta;

   // Itrate over the input string
   for(int i=0;i<s.length();i++)
   {
      // If ith element is opening bracket then push
      if(s[i]=='(' or s[i]=='[' or s[i]=='{')
      {
         sta.push(s[i]);
      }

      // Else it is a closing bracket
      else
      {
         // Check if stack is not empty this avoids runtime error
         if(sta.empty()){return false;}

         // Now check if the top of stack contains corresponding opening bracket 
         //If yes the pop it else return false

         if(s[i]==')')
         {
            if(sta.top()=='('){sta.pop();}
            else{return false;}
         }
         if(s[i]==']')
         {
            if(sta.top()=='['){sta.pop();}
            else{return false;}
         }
         if(s[i]=='}')
         {
            if(sta.top()=='{'){sta.pop();}
            else{return false;}
         }
      }
   }

   // If stack is empty that means ecvery thing is fine 
   if(sta.empty()){return true;}
   else{return false;}
}
```

### Remove Adjacent Duplicates

[Remove All Adjacent Duplicates In String - LeetCode](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)

You are given a string `s` consisting of lowercase English letters. A **duplicate removal** consists of choosing two **adjacent** and **equal** letters and removing them.

We repeatedly make **duplicate removals** on `s` until we no longer can.

```
Input: s = "abbaca"
Output: "ca"
Explanation:
For example, in "abbaca" we could remove "bb" since the letters are adjacent and equal, and this is the only possible move.  The result of this move is that the string is "aaca", of which only "aa" is possible, so the final string is "ca".

Input: s = "azxxzy"
Output: "ay"
```

### Approach:

1. Iterate over the input array
2. If the `Ith` element and the top element of stack is same then pop it.
3. or else push it
4. Then iterate over the stack and add each element in an empty string
5. Reverse the string and return it.

```cpp
string removeDuplicates(string s)
{
   stack<char> sta;

   // Empty staring to store answer in the end
   string ans = "";

   // Loop over input string
   for(int i=0;i<s.size();i++)
   {
      // if stack is empty then its the first element (i=0)
      // If s[i]!=sta.top() then the next and previous element is same
      if(sta.empty() or s[i]!=sta.top()){sta.push(s[i]);}
      else
      {
         sta.pop();
      }
   }

   //itrate over the stack
   while(!sta.empty())
   {
      // add elements of stack in emepty string
      ans.push_back(sta.top());
      sta.pop();
   }

   // Reverse the final ans sting bcz the first element will be last element in stack while poping
   reverse(ans.begin(), ans.end());
   return ans;
}
```

## Patrice problems:

### Basic Problems -

[Reverse the Words of a String using Stack - GeeksforGeeks](https://www.geeksforgeeks.org/reverse-the-sentence-using-stack/)

### Standard Problems -

[Balanced Parantheses! - InterviewBit](https://www.interviewbit.com/problems/balanced-parantheses/)

[Reverse a stack using recursion - GeeksforGeeks](https://www.geeksforgeeks.org/reverse-a-stack-using-recursion/)

[Next Greater Element - GeeksforGeeks](https://www.geeksforgeeks.org/next-greater-element/)

[Next Smaller Element - GeeksforGeeks](https://www.geeksforgeeks.org/next-smaller-element/)

[Nearest Smaller Element - InterviewBit](https://www.interviewbit.com/problems/nearest-smaller-element/)

---

### CP Problems -

[Little Shino and Pairs | Practice Problems](https://www.hackerearth.com/practice/data-structures/stacks/basics-of-stacks/practice-problems/algorithm/little-shino-and-pairs/)

[Contest Page | CodeChef](https://www.codechef.com/problems/COMPILER)

[Problem - C - Codeforces](https://codeforces.com/contest/5/problem/C)

[Problem - C - Codeforces](https://codeforces.com/contest/797/problem/C)

[SPOJ.com - Problem JNEXT](https://www.spoj.com/problems/JNEXT/)

[Largest Rectangle in Histogram - LeetCode](https://leetcode.com/problems/largest-rectangle-in-histogram/)

[Contest Page | CodeChef](https://www.codechef.com/LTIME94B/problems/LUNCHTIM)

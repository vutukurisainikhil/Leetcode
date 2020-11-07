```cpp Question
You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Follow up:
What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

Example:

Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7
```

#**CPP CODE**

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
        stack<int> s1;
        stack<int> s2;
        ListNode* temp = l1;
        while(l1!=NULL){
            s1.push(l1->val);
            l1 = l1->next;
        }
        temp = l2;
        while(l2!=NULL){
            s2.push(l2->val);
            l2 = l2->next;
        }
        stack<int> sum;
        int extra=0;
        // Adding two stack values for most significant bit
        while(!s1.empty() && !s2.empty()){
            int x=s1.top();
            s1.pop();
            int y = s2.top();
            s2.pop();
            int s = x+y;
            if(extra>0){
                s = s+ extra;
                extra =0;
            }
            if(s>9){
                extra  = s/10;
                s = s%10;
            }
            //cout<<"=sum-"<<s<<endl;
            sum.push(s);
        }
        // adding existing int in stacks 
        while(!s1.empty()){
            int s = s1.top();
            s1.pop();
            if(extra>0){
                s = s+extra;
                extra =0;
            }
            if(s>9){
                extra  = s/10;
                s = s%10;
            }
            sum.push(s);
            //cout<<" *sum-"<<s<<endl;
        }
        while(!s2.empty()){
            int s = s2.top();
            s2.pop();
            if(extra>0){
                s = s+extra;
                extra =0;
            }
            if(s>9){
                extra  = s/10;
                s = s%10;
            }
            sum.push(s);
        }
        if(extra>0){
                int s =extra;
                sum.push(s);
                extra=0;
        }
        // reserving existing stack 
        while(!sum.empty()){
            s1.push(sum.top());
            sum.pop();
        }
        // returning ListNode as answer
        ListNode* result =NULL;
        while(!s1.empty()){
            ListNode *temp = new ListNode(s1.top());
            temp->next = result;
            result = temp;
            s1.pop();
        }
        return result;
    }
    
};
```

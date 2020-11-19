```cpp Question
Given an encoded string, return its decoded string.

The encoding rule is: k[encoded_string], where the encoded_string inside the square brackets is being repeated exactly k times. Note that k is guaranteed to be a positive integer.

You may assume that the input string is always valid; No extra white spaces, square brackets are well-formed, etc.

Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, k. For example, there won't be input like 3a or 2[4].

Example 1:

Input: s = "3[a]2[bc]"
Output: "aaabcbc"
Example 2:

Input: s = "3[a2[c]]"
Output: "accaccacc"
Example 3:

Input: s = "2[abc]3[cd]ef"
Output: "abcabccdcdcdef"
Example 4:

Input: s = "abc3[cd]xyz"
Output: "abccdcdcdxyz"
 

Constraints:

1 <= s.length <= 30
s consists of lowercase English letters, digits, and square brackets '[]'.
s is guaranteed to be a valid input.
All the integers in s are in the range [1, 300].
```

#**CPP CODE**

```cpp
class Solution {
public:
    stack<string> str;
    string decodeString(string s) {
        stack<string> str;
        string sub_str = "";
        string num = "";
        for(int i=0;i<s.length();i++){
            // if an small english alphabet
            if(s[i] >= 97 && s[i] <= 122){
                sub_str += s[i];
            }
            else if(isdigit(s[i])){
                num += s[i];
            }
            else if(s[i]==']'){
                int no=to_number(str.top());
                str.pop();
                string k="";
                for(int z=0;z<no;z++){
                    k +=  sub_str;
                }
                if(!str.empty()){
                    string kk = str.top();
                    str.pop();
                    sub_str= kk + k;
                }
            }
            else{
                str.push(sub_str);
                str.push(num);
                sub_str="";
                num="";
            }
        }
        return sub_str;
    }
    
    //converting string formatted digit to int format;
    int to_number(string number){
        int num=0;
        for(int i=0;i<number.size();i++){
            num = num*10+number[i]-'0';
        }
        return num;
    }
    
};
```

'''Question
Sort a linked list using insertion sort.

Algorithm of Insertion Sort:

Insertion sort iterates, consuming one input element each repetition, and growing a sorted output list.
At each iteration, insertion sort removes one element from the input data, finds the location it belongs within the sorted list, and inserts it there.
It repeats until no input elements remain.

Example 1:

Input: 4->2->1->3
Output: 1->2->3->4
Example 2:

Input: -1->5->3->4->0
Output: -1->0->3->4->5

''''

#**CPP CODE**
'''CPP
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
    ListNode* insertionSortList(ListNode* head) {
        if(head==NULL)
            return head;
        ListNode* temp = head;
        int n=1;
        while(temp->next!=NULL){
            temp=temp->next;
            n++;
        }
        temp = head;
        int x,y;
        temp = temp->next;
        for(int i=1;i<n;i++){
            ListNode* temp1=head;
            x = temp->val;
            int j=0;
            while(j<i){
                if(x < temp1->val){
                    int k=temp1->val;
                    temp1->val = x;
                    x = k;
                }
                j++;
                temp1 = temp1->next;
            }
            temp->val = x;
            temp = temp->next;
        }
      return head;
    }
};
'''

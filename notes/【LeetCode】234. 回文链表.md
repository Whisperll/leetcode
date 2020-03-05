[题目](https://leetcode-cn.com/problems/palindrome-linked-list/)
代码
```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean isPalindrome(ListNode head) {
        if(head == null) return true;
        ListNode slow = head, fast = head, pre = head, prepre = null;
        while(fast != null && fast.next != null){
            pre = slow;
            slow = slow.next;
            fast = fast.next.next;
            pre.next = prepre;
            prepre = pre;
        }
        if(fast != null){
            slow = slow.next;
        }
        while(pre != null && slow != null){
            if(pre.val != slow.val){
                return false;
            }
            slow = slow.next;
            pre = pre.next;
        }
        return true;
    }
}
```

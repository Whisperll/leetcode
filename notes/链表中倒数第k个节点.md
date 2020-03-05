# [题目](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)
## 思路：快慢指针
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
    public ListNode getKthFromEnd(ListNode head, int k) {
        if(head == null) return null;
        ListNode fast = head, slow = head;
        while(k != 0){
            fast = fast.next;
            k--;
        }
        while( fast != null){
            fast = fast.next;
            slow = slow.next;
        }
        return slow;
    }
}
```

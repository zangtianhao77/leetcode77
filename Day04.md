# Day04 Linked-list part2
## (1) 24. Swap Nodes in Pairs
Problem (24): https://leetcode.cn/problems/swap-nodes-in-pairs/

Solution: https://programmercarl.com/0024.%E4%B8%A4%E4%B8%A4%E4%BA%A4%E6%8D%A2%E9%93%BE%E8%A1%A8%E4%B8%AD%E7%9A%84%E8%8A%82%E7%82%B9.html

Key:
using dummy head to store the head node

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode swapPairs(ListNode head) {
        //define a dummy node
        ListNode dummyNode = new ListNode(-1, head);
        //point to dummy node
        ListNode cur = dummyNode;
        //temp points to node after the second one
        ListNode temp;
        //first points to the first node to be swapped
        ListNode first;
        //second points to the second node to be swapped (swap with first)
        ListNode second;
        //when next first and next second nodes are not null, go on looping
        while (cur.next!=null && cur.next.next!=null) {
            //temp points to node after the second one
            temp = cur.next.next.next;
            //first points to the first node to be swapped
            first = cur.next;
            //second points to the second node to be swapped (swap with first)
            second = cur.next.next;
            //begin swapping
            cur.next = second;
            second.next = first;
            first.next = temp;
            //cur to first so that begin next swap
            cur = first;
        }

        return dummyNode.next;

    }
}
```

***
## (2) 19. Remove Nth Node From End of List
Problem (19): https://leetcode.cn/problems/remove-nth-node-from-end-of-list/

Solution: https://programmercarl.com/0019.%E5%88%A0%E9%99%A4%E9%93%BE%E8%A1%A8%E7%9A%84%E5%80%92%E6%95%B0%E7%AC%ACN%E4%B8%AA%E8%8A%82%E7%82%B9.html

Key: 
* two pointers
* fast pointer is n more steps forward than slow pointer
* when fast is the last node, slow is the Nth node from end of list

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummyNode = new ListNode (-1, head);
        //define fast and slow ptrs, when fast is the last node, the slow ptr should be the one right beofre the node which should be deleted
        ListNode fast = dummyNode;
        ListNode slow = dummyNode;
        //move fast so that the interval is correct
        for (int i = 0; i < n; i++) {
            fast = fast.next;
        }
        while (fast.next!=null) {
            fast = fast.next;
            slow = slow.next;
        }
        //delete the corresponding node
        slow.next = slow.next.next;

        return dummyNode.next;
    }
}
```
***

## (3) 
Problem: https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/

Solution: https://programmercarl.com/%E9%9D%A2%E8%AF%95%E9%A2%9802.07.%E9%93%BE%E8%A1%A8%E7%9B%B8%E4%BA%A4.html

key: 
* let the last nodes of list A and list B are at the same position

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode curA = headA;
        ListNode curB = headB;
        int lenA = 0, lenB = 0;
        //calc lengths of list A and B
        while (curA != null) {
            curA = curA.next;
            lenA++;
        }
        while (curB != null) {
            curB = curB.next;
            lenB++;
        }
        curA = headA;
        curB = headB;
        if (lenA >= lenB) {
            int dif = lenA - lenB;
            //move the pointer to ensure the number of the left nodes are the same
            while (dif > 0) {
                curA = curA.next;
                dif--;
            }
            //check if there are same nodes
            while (curA!=null) {
                if (curA.val == curB.val) {
                    return curA;
                }
                curA = curA.next;
                curB = curB.next;
            }
        } else {
            int dif = lenB - lenA;
            //move the pointer to ensure the number of the left nodes are the same
            while (dif > 0) {
                curB = curB.next;
                dif--;
            }
            //check if there are same nodes
            while (curB!=null) {
                if (curA == curB) {
                    return curB;
                }
                curA = curA.next;
                curB = curB.next;
            }
        }
        return null;
    }
}
```
***

## (4) 142. Linked List Cycle II
Problem (142): https://leetcode.cn/problems/linked-list-cycle-ii/

Solution: https://programmercarl.com/0142.%E7%8E%AF%E5%BD%A2%E9%93%BE%E8%A1%A8II.html

Key: 
See illustrations in solution web

```
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {// 有环
                ListNode index1 = fast;
                ListNode index2 = head;
                // 两个指针，从头结点和相遇结点，各走一步，直到相遇，相遇点即为环入口
                while (index1 != index2) {
                    index1 = index1.next;
                    index2 = index2.next;
                }
                return index1;
            }
        }
        return null;
    }
}
```


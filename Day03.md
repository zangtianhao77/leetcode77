# Day03 Linked-list part1
## (1)  Remove Linked List Elements
Problem (203): https://leetcode.cn/problems/remove-linked-list-elements/

Solution: https://programmercarl.com/0203.%E7%A7%BB%E9%99%A4%E9%93%BE%E8%A1%A8%E5%85%83%E7%B4%A0.html

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
    public ListNode removeElements(ListNode head, int val) {
        if (head == null) {
            return head;
        }
        //set up a dummy head
        ListNode dummy = new ListNode(-1, head);
        ListNode pre = dummy;
        ListNode traverse = head;
        while(traverse!=null) {
            if (traverse.val==val) {
                pre.next = traverse.next;
            } else {
                pre = traverse;
            }
            traverse = traverse.next;
        }
        return dummy.next;
    }
}
```
***
## (2) Design Linked List
Problem (707): https://leetcode.cn/problems/design-linked-list/

Solution: https://programmercarl.com/0707.%E8%AE%BE%E8%AE%A1%E9%93%BE%E8%A1%A8.html

Key: marginal conditions
* index < 0, index > length

```
class ListNode {
    int val;
    ListNode next;
    ListNode(){};
    ListNode(int val) {
        this.val = val;
    }
}


class MyLinkedList {

    //size to store the length of the linked list
    int size;
    //head node
    ListNode head;

    public MyLinkedList() {
        size = 0;
        head = new ListNode(0);
    }
    
    public int get(int index) {
        //out of interval
        if (index < 0 || index >=size ){
            return -1;
        }
        //get val of index
        ListNode tra = head;
        for (int i = 0; i <= index; i++) {
            tra = tra.next;
        }
        return tra.val;
    }
    
    public void addAtHead(int val) {
        // ListNode newHead = new ListNode(val);
        // newHead.next = head;
        addAtIndex(0, val);
    }
    
    public void addAtTail(int val) {
        addAtIndex(size, val);
    }
    
    public void addAtIndex(int index, int val) {
        //out of range, return
        if (index > size) {
            return;
        }//negative index, return index 0
        if (index<0) {
            index = 0;
        }
        size++;
        //add node
        ListNode pre = head;
        for (int i = 0; i < index; i++) {
            pre = pre.next;
        }
        ListNode newNode = new ListNode(val);
        newNode.next = pre.next;
        pre.next = newNode;
    }
    
    public void deleteAtIndex(int index) {
        if (index < 0 || index >= size) {
            return;
        }
        size--;
        //at the first, just head to the next and return
        if (index == 0) {
            head = head.next;
            return;
        }
        //if not the first
        ListNode pre = head;
        //注意index
        for (int i = 0; i < index; i++) {
            pre = pre.next;
        }
        pre.next = pre.next.next;
    }
}

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList obj = new MyLinkedList();
 * int param_1 = obj.get(index);
 * obj.addAtHead(val);
 * obj.addAtTail(val);
 * obj.addAtIndex(index,val);
 * obj.deleteAtIndex(index);
 */
```
***
## (3) Reverse Linked List
Problem (206): https://leetcode.cn/problems/reverse-linked-list/

Solution: https://programmercarl.com/0206.%E7%BF%BB%E8%BD%AC%E9%93%BE%E8%A1%A8.html#%E5%8F%8C%E6%8C%87%E9%92%88%E6%B3%95

Key:
* define a pre to store the new next node
* Define a temp pointer to store original trav.next
* trav.next first points to pre which is null, then pre points to trav which is head

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
    public ListNode reverseList(ListNode head) {
        //define a pre to store the new next node
        ListNode pre = null;
        ListNode trav = head;
        //temp node to store original trav.next
        ListNode temp = null;
        while (trav!=null) {
            temp = trav.next;
            //trav.next first points to pre which is null, then pre points to trav which is head
            trav.next = pre;
            pre = trav;
            trav = temp;
        }

        return pre;
    }
}
```
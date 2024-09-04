# 链表-链表基础

|Date\Question|203-E|707-M|206-E|24-M|19-M|160-E|142-M|
|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|
|2024-09-03|Y|Y|Y|X|X|X|X|

## 203 Remove Linked List Elements
Given the head of a linked list and an integer val, remove all the nodes of the linked list that has Node.val == val, and return the new head.

Input: head = [1,2,6,3,4,5,6], val = 6
Output: [1,2,3,4,5]

- [X] 2024-09-03: 08:44

```c#
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int val=0, ListNode next=null) {
 *         this.val = val;
 *         this.next = next;
 *     }
 * }
 */
public class Solution {
    public ListNode RemoveElements(ListNode head, int val) {
        ListNode preHead = new ListNode(-1);
        preHead.next = head;
        ListNode prev = preHead;

        while(prev.next!=null)
        {
            if(prev.next.val == val) prev.next = prev.next.next;
            else prev = prev.next;
        }
        return preHead.next;
    }
}
```
## 707 Design Linked List
Design your implementation of the linked list. You can choose to use a singly or doubly linked list.
A node in a singly linked list should have two attributes: val and next. val is the value of the current node, and next is a pointer/reference to the next node.
If you want to use the doubly linked list, you will need one more attribute prev to indicate the previous node in the linked list. Assume all nodes in the linked list are 0-indexed.
Implement the MyLinkedList class:
MyLinkedList() Initializes the MyLinkedList object.
int get(int index) Get the value of the indexth node in the linked list. If the index is invalid, return -1.
void addAtHead(int val) Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list.
void addAtTail(int val) Append a node of value val as the last element of the linked list.
void addAtIndex(int index, int val) Add a node of value val before the indexth node in the linked list. If index equals the length of the linked list, the node will be appended to the end of the linked list. If index is greater than the length, the node will not be inserted.
void deleteAtIndex(int index) Delete the indexth node in the linked list, if the index is valid.

Example 1:
Input
["MyLinkedList", "addAtHead", "addAtTail", "addAtIndex", "get", "deleteAtIndex", "get"]
[[], [1], [3], [1, 2], [1], [1], [1]]
Output
[null, null, null, null, 2, null, 3]
Explanation
MyLinkedList myLinkedList = new MyLinkedList();
myLinkedList.addAtHead(1);
myLinkedList.addAtTail(3);
myLinkedList.addAtIndex(1, 2);    // linked list becomes 1->2->3
myLinkedList.get(1);              // return 2
myLinkedList.deleteAtIndex(1);    // now the linked list is 1->3
myLinkedList.get(1);              // return 3

- [X] 2024-09-03: 09:48

```c#
// public ListNode
// {
//     public int val;
//     public ListNode next;
//     public ListNode(int val){this.val = val;}
// }

public class MyLinkedList {
    ListNode dummyHead;
    int count;

    public MyLinkedList() {
        dummyHead = new ListNode(0);
        count = 0;
    }
    
    public int Get(int index) {
        if(index < 0 || count <= index) return -1;
        ListNode curr = dummyHead;
        for(int i = 0; i <= index;i++)
        {
            curr = curr.next;
        }
        return curr.val;
    }
    
    public void AddAtHead(int val) {
        AddAtIndex(0,val);
    }
    
    public void AddAtTail(int val) {
        AddAtIndex(count,val);
    }
    
    public void AddAtIndex(int index, int val) {
        if(index>count) return;
        index = Math.Max(0,index);
        count++;
        ListNode tmp = dummyHead;
        for(int i = 0; i < index;i++)
        {
            tmp = tmp.next;
        }
        ListNode tmp2 = new ListNode(val);
        tmp2.next = tmp.next;
        tmp.next = tmp2;

    }
    
    public void DeleteAtIndex(int index) {
        if(index >= count || index <0) return;
        count--;
        ListNode tmp = dummyHead;
        for(int i = 0; i < index;i++)
        {
            tmp = tmp.next;
        }
        tmp.next = tmp.next.next;
    }
}

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList obj = new MyLinkedList();
 * int param_1 = obj.Get(index);
 * obj.AddAtHead(val);
 * obj.AddAtTail(val);
 * obj.AddAtIndex(index,val);
 * obj.DeleteAtIndex(index);
 */
```

## 206 Reverse Linked List
Given the head of a singly linked list, reverse the list, and return the reversed list.

Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]

- [X] 2024-09-03: 03：05

```c#
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int val=0, ListNode next=null) {
 *         this.val = val;
 *         this.next = next;
 *     }
 * }
 */
public class Solution {
    public ListNode ReverseList(ListNode head) {
        ListNode prev = null, curr =head;

        while(curr!=null)
        {
            ListNode dummy = curr.next;
            // 现在指向上一个
            curr.next = prev;
            // 更新prev
            prev = curr;
            // 更新本来的下一个，以防更新到prev
            curr = dummy;
        }
        return prev;

    }
}
```

## 24 Swap Nodes in Pairs
Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

Input: head = [1,2,3,4]
Output: [2,1,4,3]

- [ ] 2024-09-03: 14:20

```c#
// 画图解决
// dummy -> 1 -> 2 -> 3
// 步骤应该是 dummy -> 2 -> 1 -> 3
public class Solution {
    public ListNode SwapPairs(ListNode head) {
        ListNode dummyHead = new ListNode();
        dummyHead.next = head;
        ListNode curr = dummyHead;

        while(curr.next!=null && curr.next.next!=null)
        {
            ListNode tmp1 = curr.next;
            ListNode tmp2 = curr.next.next.next;

            curr.next = curr.next.next;
            curr.next.next = tmp1;
            curr.next.next.next = tmp2;

            curr = curr.next.next;
        }
        return dummyHead.next;
    }
}
```
## 19 Remove Nth Node From End of List
Given the head of a linked list, remove the nth node from the end of the list and return its head.

Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]

- [ ] 2024-09-04: 19：46

// 先将fast移动到n+1
// 再将fast和slow同时移动直到fast==null
// 删除slow指向的节点
```c#public class Solution {
    public ListNode RemoveNthFromEnd(ListNode head, int n) {
        ListNode dummyHead = new ListNode(0);
        dummyHead.next = head;
        ListNode fast = dummyHead;
        ListNode slow = dummyHead;

        for(int i = 0; i <= n ; i++)
        {
            fast = fast.next;
        }

        while(fast!=null)
        {
            fast = fast.next;
            slow = slow.next;
        }

        if(slow.next!=null)slow.next = slow.next.next;

        return dummyHead.next;
    }
}
```

## 160 Intersection of Two Linked Lists
Given the heads of two singly linked-lists headA and headB, return the node at which the two lists intersect. If the two linked lists have no intersection at all, return null.

Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,6,1,8,4,5], skipA = 2, skipB = 3
Output: Intersected at '8'
Explanation: The intersected node's value is 8 (note that this must not be 0 if the two lists intersect).
From the head of A, it reads as [4,1,8,4,5]. From the head of B, it reads as [5,6,1,8,4,5]. There are 2 nodes before the intersected node in A; There are 3 nodes before the intersected node in B.
- Note that the intersected node's value is not 1 because the nodes with value 1 in A and B (2nd node in A and 3rd node in B) are different node references. In other words, they point to two different locations in memory, while the nodes with value 8 in A and B (3rd node in A and 4th node in B) point to the same location in memory.

- [ ] 2024-09-04: 06:49

// 除了用交叉判断，由于这道题交叉链表只在最尾部
// 也可以先将A和B的长度差求出，然后把尾部对齐
// 对比B（头部）和A是否相等，不相等继续后移
```c#
public class Solution {
    public ListNode GetIntersectionNode(ListNode headA, ListNode headB) {
        if(headA == null || headB == null) return null;

        ListNode pointer1 = headA;
        ListNode pointer2 = headB;

        while(pointer1!=pointer2)
        {
            pointer1 = pointer1 == null ? headB : pointer1.next;
            pointer2 = pointer2 == null ? headA : pointer2.next;
        }
        return pointer1;
    }
}
```

## 142 Linked List Cycle II
Given the head of a linked list, return the node where the cycle begins. If there is no cycle, return null.
There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to (0-indexed). It is -1 if there is no cycle. Note that pos is not passed as a parameter.
Do not modify the linked list.

Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.

- [ ] 2024-09-04: 05:09

// 相遇 = slow(每次一步) == fast(每次两步)
// 相遇的地点 = slow从相遇点开始走，fast从head开始走
![image](https://github.com/user-attachments/assets/47de3a9a-543a-47a1-8a51-97a5b5c05b27)

```c#
public class Solution {
    public ListNode DetectCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;

        while(fast!=null && fast.next!=null)
        {
            slow = slow.next;
            fast = fast.next.next;

            if(fast == slow)
            {
                fast = head;
                while(fast!=slow)
                {
                    fast = fast.next;
                    slow = slow.next;
                }
                return fast;
            }
            
        }
        return null;
        
    }
}
```

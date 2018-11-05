---
layout: post
title: Algorithms LinkedList 01
categories: Algorithms
description: Algorithms LinkedList 01
keywords: Algorithms, LinkedList
---

#### [Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)

```java
/*
Solution 1

Time complexity: O(n);
Space complexity: O(n);

*/
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        Map<Integer, ListNode> map = new HashMap<>();
        ListNode dump = new ListNode(0);
        dump.next = head;
        map.put(0, dump);
        int i = 1;
        while (true) {
            if (head == null)
                break;
            map.put(i, head);
            i++;
            head = head.next;
        }
        i--;
        map.get(i - n).next = map.get(i - n + 1).next;
        return map.get(0).next;
    }
}


/*

Solution 2

Time complexity: O(n);
Space complexity: O(1);
2018-11-01 19:12:31

*/

class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        int num = 0;
        ListNode temp = new ListNode(0);
        ListNode dump = new ListNode(0);
        dump.next = head;
        temp.next = head;
        while (true) {
            if (temp.next == null)
                break;
            num++;
            temp = temp.next;
        }
        temp = dump;
        for (int i = 0; i < num - n; i++) {
            temp = temp.next;
        }

        temp.next = temp.next.next;
        return dump.next;

    }
}
```

#### [Rotate List](https://leetcode.com/problems/rotate-list/description/)

```java
/*

Time complexity: O(n);
Space complexity:O(1);
2018-11-01 19:34:20

*/
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        ListNode dump = new ListNode(0);
        ListNode temp = new ListNode(0);
        dump.next = head;
        temp.next = head;
        int num = 0;
        while(true){
            if(temp.next == null)
                break;
            num++;
            temp = temp.next;
        }
        if(num == 0)
            return dump.next;
        ListNode end = temp;
        temp = dump;
        k = k % num;
        for(int i = 0; i < num - k; i++){
            temp = temp.next;
        }
        
        end.next = dump.next;
        dump.next = temp.next;
        temp.next = null;
        return dump.next;
    }
}
```

#### [Remove Duplicates from Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list/description/)

```java
/*

Time complexity: O(n);
Space complexity: O(1);
2018-11-01 20:54:35

*/
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if(head == null)
            return head;
        ListNode dump = new ListNode(0);
        dump.next = head;
        ListNode p = head;
        ListNode r = head.next;
        
        while(true){
            if(r == null)
                break;
            if(p.val == r.val){
                p.next = r.next;
                r = r.next;
            }else{
                p = p.next;
                r = r.next;
            }
        }
        return dump.next;
    }
}
```


#### [Remove Duplicates from Sorted List II](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/description/)

```java
/*
Time complexity: O(n);
Space complexity: O(1);
2018-11-01 20:40:53

*/

class Solution{
    public ListNode deleteDuplicates(ListNode head){
        if(head == null)
            return head;
        ListNode dump = new ListNode(0);
        ListNode p = dump;
        ListNode r = head;
        dump.next = head;
        
        while(true){
            if(r == null)
                break;
            while(true){
                if(r.next!=null&&r.val==r.next.val){
                    r = r.next;
                }else{
                    break;
                }
            }
            
            if(p.next == r){
                r = r.next;
                p = p.next;
            }else{
                p.next = r.next;
                r = r.next;
            }
        }
        return dump.next;
    }
}
```

#### [Partition List](https://leetcode.com/problems/partition-list/description/)

```java
/*

Time complexity: O(n);
Space complexity: O(1);
2018-11-01 21:05:45

*/
class Solution {
    public ListNode partition(ListNode head, int x) {
        if(head == null)
            return head;
        
        ListNode dump1 = new ListNode(0);
        ListNode cur1 = dump1;
        ListNode dump2 = new ListNode(0);
        ListNode cur2 = dump2;
        
        ListNode p = head;
        
        while(true){
            if(p == null)
                break;
            if(p.val < x){
                cur1.next = p;
                cur1 = p;
            }else{
                cur2.next = p;
                cur2 = p;
            }
            p = p.next;
            cur1.next = null;
            cur2.next = null;
        }
        
        cur1.next = dump2.next;
        return dump1.next;
    }
}
```
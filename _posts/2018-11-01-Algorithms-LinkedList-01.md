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
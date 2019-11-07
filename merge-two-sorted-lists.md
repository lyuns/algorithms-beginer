# 刷题日记

### https://leetcode-cn.com/problems/merge-two-sorted-lists

> 21. 合并两个有序链表 将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。

1. 暴力解法

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* head = new ListNode(0);
        ListNode* p = head;
        while (l1 != NULL && l2 != NULL) {
            int cur;
            if (l1 -> val < l2 -> val) {
                cur = l1 -> val;
                l1 = l1 -> next;
            } else {
                cur = l2 -> val;
                l2 = l2 -> next;
            }
            p -> next = new ListNode(cur);
            p = p -> next;
        }
        while (l1 != NULL) {
            p -> next = new ListNode(l1 -> val);
            l1 = l1 -> next;
            p = p -> next;
        }
        while (l2 != NULL) {
            p -> next = new ListNode(l2 -> val);
            l2 = l2 -> next;
            p = p -> next;
        }
        return head -> next;
    }
};
```
解题思路：

- 两个有序链表均不为空时，依次取链表中最小的值存入新链表（起始位置放置了一个占位结点）
- 当有一个链表为空时，依次将不为空的链表值存入新链表的末尾
- 因为起始位置放置了占位结点，次数头结点位占位结点的下一位

附加：时间复杂度O(n), 空间复杂度O(n)，后续思考更优解。

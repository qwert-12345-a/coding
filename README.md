# Merge k Sorted Lists (LeetCode 23)

## Problem Description
Given an array of linked lists, each linked list is sorted in ascending order. Merge all the linked lists into one sorted linked list and return it.

**Example 1:**
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]

**Example 2:**
Input: lists = []
Output: []

**Example 3:**
Input: lists = [[]]
Output: []

**Constraints:**
- k == lists.length
- 0 <= k <= 10^4
- 0 <= lists[i].length <= 500
- -10^4 <= lists[i][j] <= 10^4
- Each lists[i] is sorted in ascending order
- The total number of all nodes does not exceed 10^4

## Solution Approach
This problem is a classic example of multi-way merging. Since each list is already sorted, we can use a min-heap (priority queue) to efficiently merge all the lists:

1. Push the head node of each list into the min-heap.
2. Each time, pop the smallest node from the heap and append it to the result list.
3. If the popped node has a next node, push the next node into the heap.
4. Repeat the process until the heap is empty.

Time complexity: O(N log k), where N is the total number of nodes and k is the number of lists.

## Code Implementation
See `solution.cpp` for the full implementation. The core code is as follows:

```
class Solution {
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        auto cmp = [](ListNode* a, ListNode* b) { return a->val > b->val; };
        priority_queue<ListNode*, vector<ListNode*>, decltype(cmp)> pq(cmp);
        for (auto node : lists) {
            if (node) pq.push(node);
        }
        ListNode dummy(0);
        ListNode* tail = &dummy;
        while (!pq.empty()) {
            ListNode* node = pq.top(); pq.pop();
            tail->next = node;
            tail = tail->next;
            if (node->next) pq.push(node->next);
        }
        return dummy.next;
    }
};
```

## Summary
This problem tests the application of linked lists, priority queues, and the idea of multi-way merging. The priority queue efficiently maintains the smallest node among all current lists, ensuring the overall order.

---
title: Road Map Solution
categories: Leetcode
tags:
- Leetcode
---

- [Solution](#solution)
  - [Two Pointers](#two-pointers)
    - [Valid Palindrome](#valid-palindrome)
    - [680. Valid Palindrome II](#680-valid-palindrome-ii)
      - [Naive one based on Valid Palindrome I](#naive-one-based-on-valid-palindrome-i)
    - [Closest Sum](#closest-sum)
    - [3Sum](#3sum)
    - [Best Time to Buy and Sell Stock](#best-time-to-buy-and-sell-stock)
    - [209. Minimum Size Subarray Sum](#209-minimum-size-subarray-sum)
    - [3. Longest Substring Without Repeating Characters](#3-longest-substring-without-repeating-characters)
    - [904. Fruit Into Baskets](#904-fruit-into-baskets)
      - [基于最长连续水果类型的解法](#基于最长连续水果类型的解法)
      - [基于sliding windows的解法（Recommended）](#基于sliding-windows的解法recommended)
    - [567. Permutation in String](#567-permutation-in-string)
    - [1493. Longest Subarray of 1's After Deleting One Element](#1493-longest-subarray-of-1s-after-deleting-one-element)
      - [手动记录zero\_idx](#手动记录zero_idx)
      - [不记录zero\_idx, 让left递增直到zero\_idx](#不记录zero_idx-让left递增直到zero_idx)
    - [Interval](#interval)
      - [986. Interval List Intersections](#986-interval-list-intersections)
      - [57. Insert Interval](#57-insert-interval)
      - [56. Merge Intervals](#56-merge-intervals)
    - [Linked List Manipulation](#linked-list-manipulation)
      - [24. Swap Nodes in Pairs](#24-swap-nodes-in-pairs)
      - [234. Palindrome Linked List](#234-palindrome-linked-list)
      - [92. Reverse Linked List II](#92-reverse-linked-list-ii)
      - [61. Rotate List](#61-rotate-list)
      - [328. Odd Even Linked List](#328-odd-even-linked-list)
      - [143. Reorder List](#143-reorder-list)
    - [Hash Maps](#hash-maps)
      - [205. Isomorphic Strings](#205-isomorphic-strings)
      - [290. Word Pattern](#290-word-pattern)
      - [49. Group Anagrams](#49-group-anagrams)
      - [438. Find All Anagrams in a String](#438-find-all-anagrams-in-a-string)
      - [974. Subarray Sums Divisible by K](#974-subarray-sums-divisible-by-k)
    - [Modified Binary Search](#modified-binary-search)
      - [278. First Bad Version](#278-first-bad-version)
      - [2529. Maximum Count of Positive Integer and Negative Integer](#2529-maximum-count-of-positive-integer-and-negative-integer)
      - [33. Search in Rotated Sorted Array](#33-search-in-rotated-sorted-array)
      - [153. Find Minimum in Rotated Sorted Array](#153-find-minimum-in-rotated-sorted-array)
      - [162. Find Peak Element](#162-find-peak-element)
    - [Top K Elements](#top-k-elements)
      - [堆](#堆)
      - [703. Kth Largest Element in a Stream](#703-kth-largest-element-in-a-stream)
      - [215. Kth Largest Element in an Array](#215-kth-largest-element-in-an-array)
      - [973. K Closest Points to Origin](#973-k-closest-points-to-origin)
      - [347. Top K Frequent Elements](#347-top-k-frequent-elements)
      - [358. Rearrange String k Distance Apart](#358-rearrange-string-k-distance-apart)
    - [Sliding Window](#sliding-window)
      - [239. Sliding Window Maximum](#239-sliding-window-maximum)
      - [480. Sliding Window Median](#480-sliding-window-median)
    - [Two Heaps](#two-heaps)
      - [1985. Find the Kth Largest Integer in the Array](#1985-find-the-kth-largest-integer-in-the-array)
      - [4. Median of Two Sorted Arrays](#4-median-of-two-sorted-arrays)
      - [378. Kth Smallest Element in a Sorted Matrix](#378-kth-smallest-element-in-a-sorted-matrix)
        - [大根堆](#大根堆)
        - [二分搜索（最优性能）](#二分搜索最优性能)
    - [K-way merge](#k-way-merge)
    - [Backtracking](#backtracking)
      - [78. Subsets](#78-subsets)
      - [90. Subsets II](#90-subsets-ii)
      - [39. Combination Sum](#39-combination-sum)
      - [40. Combination Sum II](#40-combination-sum-ii)
      - [113. Path Sum II](#113-path-sum-ii)
      - [131. Palindrome Partitioning](#131-palindrome-partitioning)
      - [22. Generate Parentheses](#22-generate-parentheses)
      - [17. Letter Combinations of a Phone Number](#17-letter-combinations-of-a-phone-number)
      - [1079. Letter Tile Possibilities](#1079-letter-tile-possibilities)
      - [79. Word Search](#79-word-search)
    - [Greedy](#greedy)
      - [455. Assign Cookies](#455-assign-cookies)
    - [DFS](#dfs)
      - [1079. Letter Tile Possibilities](#1079-letter-tile-possibilities-1)
      - [104. Maximum Depth of Binary Tree](#104-maximum-depth-of-binary-tree)
      - [94. Binary Tree Inorder Traversal](#94-binary-tree-inorder-traversal)
      - [207. Course Schedule](#207-course-schedule)
        - [拓扑法](#拓扑法)



# Solution
## Two Pointers

### Valid Palindrome
```java
// Use built-in replaceAll
class Solution {
    public boolean isPalindrome(String s) {
        s = s.toLowerCase().replaceAll("[^a-zA-Z0-9]", "");

        int forward = 0;
        int backward = s.length() - 1;

        while (backward > forward) {
            if (s.charAt(forward) != s.charAt(backward)) {
                return false;
            }
            forward++;
            backward--;
        }

        return true;
    }
}
```

```java
// Self implemented support fns
class Solution {
    public boolean isPalindrome(String s) {
        char[] charArray = s.toCharArray();
        int forward = 0;
        int backward = charArray.length - 1;

        while (backward > forward) {
            // Skip non-alphanumeric characters from the beginning
            while (forward < charArray.length && !isAlphanumeric(charArray[forward])) {
                forward++;
            }
            
            // Skip non-alphanumeric characters from the end
            while (backward >= 0 && !isAlphanumeric(charArray[backward])) {
                backward--;
            }

            // Compare characters (case-insensitive)
            if (forward < charArray.length && backward >= 0 && toLowerCase(charArray[forward]) != toLowerCase(charArray[backward])) {
                return false;
            }
            forward++;
            backward--;
        }

        return true;
    }

    private boolean isAlphanumeric(char c) {
        return (c >= 'a' && c <= 'z') 
            || (c >= 'A' && c <= 'Z') 
            || (c >= '0' && c <= '9');
    }

    private char toLowerCase(char c) {
        if (c >= 'A' && c <= 'Z') {
            // Convert uppercase to lowercase by adding the ASCII offset
            return (char) (c + 'a' - 'A');
        }
        return c;
    }
}
```

### 680. Valid Palindrome II
#### Naive one based on Valid Palindrome I
```java
class Solution {
    public boolean validPalindrome(String s) {
        int left = 0;
        int right = s.length() - 1;

        while (left < right) {
            // Allow skip once.
            if (s.charAt(left) != s.charAt(right)) {
                return isPalindrome(s, left + 1, right) || isPalindrome(s, left, right - 1);
            }
            left++;
            right--;
        }

        return true;
    }

    private boolean isPalindrome(String s, int left, int right) {
        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }
}
```

### Closest Sum
```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int begin = 0;
        int end = numbers.length - 1;

        while (begin < end) {
            int sum = numbers[begin] + numbers[end];
            if (sum == target) {
                return new int[] {begin + 1, end + 1};
            }

            if (sum > target) {
                end--;
            } else {
                begin++;
            }
        }

        return null;
    }
}
```

```java
// BF
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for(int i=1;i<nums.length;i++)
        {
            for(int j=i;j<nums.length;j++)
            {
                if(nums[j-i]+nums[j]==target)
                {
                    return new int[]{j-i,j};
                }
            }
        }
        return null;
        
    
    }
}
```

```java
// HashMap
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];

            if (map.containsKey(complement)) {
                return new int[] {i, map.get(complement)};
            }

            map.put(nums[i], i);
        }

        return null;
    }
}
```

### 3Sum
```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        // Note: B-I sort 
        Arrays.sort(nums);
        List<List<Integer>> ret = new ArrayList<>();

        int n = nums.length;

        for (int i = 0; i < n - 2; i++) {
            // Skip duplicates
            if (i > 0 && nums[i] == nums[i - 1]) { continue;}

            int begin = i + 1;
            int end = n - 1;
            // 如果是要求sum为value，这里可以做修改适配
            int target = -nums[i];

            while (begin < end) {
                int sum = nums[begin] + nums[end];
                if (sum == target) {
                    ret.add(Arrays.asList(nums[i], nums[begin], nums[end]));
                    // Skip duplicates
                    while (begin < end && nums[begin] == nums[begin + 1]) {
                        begin++;
                    }
                    while (begin < end && nums[end] == nums[end - 1]) {
                        end--;
                    }

                    begin++;
                    end--;
                } else if (sum < target) {
                    begin++;
                } else {
                    end--;
                }
            }
            
        }

        return ret;
    }
}

```

### Best Time to Buy and Sell Stock
> 用双指针 O(n^2) 太高。

```java
class Solution {
    public int maxProfit(int[] prices) {
        int maxProfit = 0;
        // 可以代表在i天卖出时可能得最大收益
        int curProfit = 0;

        for (int i = 1; i < prices.length; i++) {
            int interval = prices[i] - prices[i - 1];
            // 如果为负，说明i是一个低价，低到在其之前任何一天买入在i卖出都是亏的
            // 所以it's better to start over at i
            curProfit = Math.max(0, interval + curProfit);
            maxProfit = Math.max(curProfit, maxProfit);
        }

        return maxProfit;
    }
}
```


### 209. Minimum Size Subarray Sum
```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int left = 0;
        int right = 0;
        int sum = 0;
        int minLength = Integer.MAX_VALUE;

        for (; right < nums.length; right++) {
            sum += nums[right];
            // 只有在sum大于等于过target时才记录minLength
            // 如果全程都没有大于等于过，需要最后将minLength处理为0
            boolean needUpdate = false;

            while (sum >= target) {
                sum -= nums[left];
                left++;
                needUpdate = true;
            }

            if (needUpdate) {
                minLength = Math.min(minLength, right - left + 2);
            }
        }

        return minLength == Integer.MAX_VALUE ? 0 : minLength;
    }
}
```

### 3. Longest Substring Without Repeating Characters
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int len = s.length();
        int maxLength = 0;
        Map<Character, Integer> map = new HashMap<>();
        int left = 0;

        for (int right = 0; right < len; right++) {
            char currentChar = s.charAt(right);
            
            // 如果当前子字符串中没有看到当前字符
            // 或者它出现在当前左指针之前，它是当前子字符串的一部分。
            if (map.getOrDefault(currentChar, -1) < left) {
                maxLength = Math.max(maxLength, right - left + 1);
            } else {
                // 如果该字符已被看到并且在当前子字符串中，
                // 将左指针更新到该字符最后一次出现后的位置。
                left = map.get(currentChar) + 1;
            }
            
            map.put(currentChar, right);
        }

        return maxLength;
    }
}
```


### 904. Fruit Into Baskets
> 内核: 找一个最长的仅有两种元素组成的子串

#### 基于最长连续水果类型的解法
```java
class Solution {
    public int totalFruit(int[] fruits) {
        int maxFruits = 0;           // Initialize the maximum number of fruits to be collected.
        int lastFruit = -1;          // Type of the last fruit in the second basket.
        int secondLastFruit = -1;    // Type of the last fruit in the first basket.
        int lastFruitCount = 0;      // Number of contiguous fruits of the last type.
        int currentMax = 0;          // Current maximum number of fruits.

        for (int fruit : fruits) {
            if (fruit == secondLastFruit || fruit == lastFruit) {
                // If the current fruit is the same as one of the fruits in the baskets, 
                // add it to the currentMax because it can be collected.
                currentMax++;
            } else {
                // If the current fruit is different from the fruits in the baskets,
                // we need to start collecting a new type of fruit. In this case, 
                // we consider the last fruit count plus the current fruit as the new 
                // maximum, and reset the currentMax.
                currentMax = lastFruitCount + 1;
            }

            if (fruit == lastFruit) {
                // If the current fruit is the same as the last fruit, increment the 
                // count of contiguous fruits of this type.
                lastFruitCount++;
            } else {
                // If the current fruit is different from the last fruit, it becomes 
                // the new last fruit, and we reset the last fruit count to 1.
                lastFruitCount = 1;
                secondLastFruit = lastFruit;
                lastFruit = fruit;
            }

            // Update the maximum number of fruits that can be collected.
            maxFruits = Math.max(maxFruits, currentMax);
        }

        return maxFruits;  // Return the maximum number of fruits that can be collected.
    }
}
```

#### 基于sliding windows的解法（Recommended）
```java
class Solution {
    public int totalFruit(int[] fruits) {
        Map<Integer, Integer> map = new HashMap<>();  // Create a HashMap to store fruit counts.
        int left = 0;  // Initialize the left pointer for the sliding window.
        int right = 0;  // Initialize the right pointer for the sliding window.
        int len = fruits.length;  // Get the length of the input array.
        int ret = 0;

        for (; right < len; right++) {
            map.put(fruits[right], map.getOrDefault(fruits[right], 0) + 1);

            // 从left端逐个移除fruit
            while (map.size() > 2) {
                // map中减少该水果数量
                map.put(fruits[left], map.get(fruits[left]) - 1);
                // 如果减少到0了，剔除该键值对
                // 说明当前篮子可以装入新的水果种类
                if (map.get(fruits[left]) == 0) {
                    map.remove(fruits[left]);
                }

                left++;
            }

            ret = Math.max(ret, right - left + 1);
        }

        return ret;
    }
}
```

### 567. Permutation in String
> 1. 用toCharArray代替charAt，提高速度
> 2. 只构建一次count_s2，然后每次循环用滑动窗口更新改数组


```java
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        int len_s1 = s1.length();
        int len_s2 = s2.length();

        char[] char_s1 = s1.toCharArray();
        char[] char_s2 = s2.toCharArray();
        
        if (len_s1 > len_s2) {
            return false;
        }

        int[] count_s1 = new int[26];
        int[] count_s2 = new int[26];
        
        // Initialize the count_s1 and the first window in s2
        for (int i = 0; i < len_s1; i++) {
            count_s1[char_s1[i] - 'a']++;
            count_s2[char_s2[i] - 'a']++;
        }
        
        // 优化后方案： 只构建一次count_s2，然后每次循环用滑动窗口更新改数组
        for (int i = 0; i < len_s2 - len_s1; i++) {
            if (isSameArr(count_s1, count_s2)) {
                return true;
            }

            // Key!!!
            // 滑动一格后将滑出的char数量--，滑进的char数量++即可
            count_s2[char_s2[i] - 'a']--;
            count_s2[char_s2[i + len_s1] - 'a']++;
        }
        
        // 被优化前的：每次循环都重新构建count_s2数组
        // for (int i = 0; i <= len_s2 - len_s1; i++) {
        //     int[] count_s2 = new int[26];
        //     for (int j = 0; j < len_s1; j++) {
        //         count_s2[char_s2[i+j] - 'a']++;
        //     }

        //     if (isSameArr(count_s1, count_s2)) {
        //         return true;
        //     }
        // }

        // Check the last window
        return isSameArr(count_s1, count_s2);
    }

    private boolean isSameArr(int[] arrA, int[] arrB) {
        for (int i = 0; i < arrA.length; i++) {
            if (arrA[i] != arrB[i]) {
                return false;
            }
        }

        return true;
    }
}
```

### 1493. Longest Subarray of 1's After Deleting One Element
#### 手动记录zero_idx
```java
class Solution {
    public int longestSubarray(int[] nums) {
        int len = nums.length;
        int left = 0;
        int right = 0;
        int zero_idx = 0;
        int zero_count = 0;
        int ret = 0;

        for (; right < len; right++) {
            if (nums[right] == 0) {
                if (zero_count > 0) {
                    left = zero_idx + 1;
                    zero_idx = right;
                } else {
                    zero_idx = right;
                    zero_count++;
                }
            }

            ret = Math.max(ret, right - left);
        }

        return ret;
    }
}
```
#### 不记录zero_idx, 让left递增直到zero_idx
```java
class Solution {
    public int longestSubarray(int[] nums) {
        int len = nums.length;
        int left = 0;
        int right = 0;
        int zero_count = 0;
        int ret = 0;

        for (; right < len; right++) {
            if (nums[right] == 0) {
                zero_count++;

                while (zero_count > 1) {
                    if (nums[left] == 0) {
                        zero_count--;
                    }
                    left++;
                }
            }

            ret = Math.max(ret, right - left);
        }

        return ret;

    }
}
```

### Interval

#### 986. Interval List Intersections

- `List<int[]>` 存储结果，`.toArray(new int[result.size()][])` 返回结果处理
- 双指针指向第一维，用于选取interval
- 循环条件是任一指针遍历到最后一个interval
- 通过两组start，end来截取intersection的start，end
- 判断是否加入结果
- 根据end大小判断哪个指针跳入下个interval

```java
class Solution {
    public int[][] intervalIntersection(int[][] firstList, int[][] secondList) {
        // Create a list to store the result intervals
        List<int[]> result = new ArrayList<>();
        
        // Initialize two pointers, one for each input list
        int i = 0, j = 0;

        // Iterate through both lists
        while (i < firstList.length && j < secondList.length) {
            // Get the start and end points of the current intervals in both lists
            int start1 = firstList[i][0];
            int end1 = firstList[i][1];
            int start2 = secondList[j][0];
            int end2 = secondList[j][1];

            // Find the intersection of the two intervals
            int intersectionStart = Math.max(start1, start2);
            int intersectionEnd = Math.min(end1, end2);

            // If there is an intersection (i.e., valid interval), add it to the result
            if (intersectionStart <= intersectionEnd) {
                result.add(new int[]{intersectionStart, intersectionEnd});
            }

            // Move the pointer that points to the interval with the smaller endpoint
            if (end1 < end2) {
                i++; // Move the pointer for the first list
            } else {
                j++; // Move the pointer for the second list
            }
        }

        // Convert the result list to a 2D array and return it as the final result
        return result.toArray(new int[result.size()][]);
    }
}

```

#### 57. Insert Interval

- left, right的初始取值应该直接用newInterval，可以适配一些特殊场景如：intervals = [], newInterval = [5,7]
- hasInserted标记， 用于在`第一次right < start` 或 `newInterval[1] >= intervals的最右端`时添加overlap interval
- 存在overlap的场景处理

```java
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {        
        
        List<int[]> ret = new ArrayList<>();

        // 注意初始化取值，对特殊intervals也能适配
        int left = newInterval[0];
        int right = newInterval[1];

        boolean hasInserted = false;

        for (int i = 0; i < intervals.length; i++) {
            int start = intervals[i][0];
            int end = intervals[i][1]; 

            if (left > end) {
                // 当前interval 完全在 newInterval 左边
                ret.add(intervals[i]);
            } else if (right < start) {
                // 当前interval 完全在 newInterval 右边
                if (!hasInserted) {
                    // 如果有这种interval，先添加overlap的interval
                    // 用标记防止对每个这种interval都插入overlap的interval
                    // 即是在仅遇到第一个时添加
                    ret.add(new int[] {left, right});
                    hasInserted = true;
                }
                ret.add(intervals[i]);
            } else {
                // 存在overlap的场景
                left = Math.min(left, start);
                right = Math.max(right, end);
            }

        }

        if (!hasInserted) {
            ret.add(new int[] {left, right});
        }

        return ret.toArray(new int[ret.size()][]);
    }
}
```

#### 56. Merge Intervals

- 根据start排序整个二维数组
- 用currentInterval来跨越多个overlap interval，初始值为intervals[0]
- 循环从i=1开始

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        if (intervals.length <= 1) {
            return intervals; // No merging needed for 0 or 1 interval.
        }

        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0])); // Sort by start times.

        List<int[]> ret = new ArrayList<>();
        int[] currentInterval = intervals[0];

        for (int i = 1; i < intervals.length; i++) {
            int currentEnd = currentInterval[1];
            int nextStart = intervals[i][0];
            int nextEnd = intervals[i][1];

            if (currentEnd >= nextStart) {
                // Intervals overlap or are adjacent, so we merge them.
                currentInterval[1] = Math.max(currentEnd, nextEnd);
            } else {
                // Intervals don't overlap, so we add the current interval to the result and update it to the next interval.
                ret.add(currentInterval);
                currentInterval = intervals[i];
            }
        }

        // Add the last ret interval.
        ret.add(currentInterval);

        return ret.toArray(new int[ret.size()][]);
    }
}


```


### Linked List Manipulation
#### 24. Swap Nodes in Pairs

- 用prev, left, right, after来做swap
- Extreme case: one-element and empty list
- Boundary: after is null circumstances.

```java
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

        if (null == head || null == head.next) {
            return head;
        }
        
        ListNode left = head;
        ListNode right = left.next;

        ListNode new_head = right;

        ListNode prev = head;
        ListNode after = head;

        while (null != left && null != right) {
            // Update after
            after = right.next;

            // Swap ref
            prev.next = right;
            right.next = left;
            left.next = after;

            // Update prev and left
            prev = left;
            left = after;

            // In case that `after` is null casuing after.next NPE
            if (null != after) {
                right = after.next;
            } else {
                right = null;
            }
            
        }

        return new_head;
    }
}
```

#### 234. Palindrome Linked List

1. 遍历两次，辅助int[]
- 用array记录前半的val

```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        // Count the number of nodes in the linked list
        int count = 0;
        ListNode node = head;
        while (node != null) {
            count++;
            node = node.next;
        }
        
        // Create an array to store the first half of the values
        int[] arr = new int[count / 2];
        
        // Reset the node to the head of the linked list
        node = head;
        
        // Store the values of the first half in the array
        for (int i = 0; i < arr.length; i++) {
            arr[i] = node.val;
            node = node.next;
        }
        
        // If the total count is odd, move to the next node
        if (count % 2 != 0) {
            node = node.next;
        }
        
        // Compare the values in the array with the second half of the linked list
        for (int i = arr.length - 1; i >= 0; i--) {
            if (node.val != arr[i]) {
                return false;
            }
            node = node.next;
        }
        
        return true;
    }
}

```

2. 遍历一次快慢指针，stack辅助

- 快慢指针
- 快慢指针处理奇数list中间点的方式

```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        Stack<Integer> stack = new Stack<>();
        ListNode node = head;

        ListNode slow = head;
        ListNode fast = head;

        // Find the middle of the linked list
        while (fast != null && fast.next != null) {
            stack.push(slow.val);
            slow = slow.next;
            fast = fast.next.next;
        }

        
        if (null != fast) { // List有奇数个node, slow跳过中间点
            slow = slow.next;
        }

        while (null != slow) {
            if (slow.val != stack.pop()) {
                return false;
            }
            slow = slow.next;
        }

        return true;
    }
}
```

1. 遍历一次快慢指针, 后半reverse

- `reverseList` 方法可复用

```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        if (head == null || head.next == null) {
            return true; // An empty list or a list with one node is considered a palindrome.
        }

        ListNode slow = head;
        ListNode fast = head;

        // Find the middle of the linked list
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        // Reverse the second half of the linked list
        ListNode secondHalf = reverseList(slow);

        // Compare the first half and the reversed second half
        ListNode firstHalf = head;
        while (secondHalf != null) {
            if (firstHalf.val != secondHalf.val) {
                return false;
            }
            firstHalf = firstHalf.next;
            secondHalf = secondHalf.next;
        }

        return true;
    }

    private ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode current = head;

        while (current != null) {
            ListNode next = current.next;
            current.next = prev;
            prev = current;
            current = next;
        }

        return prev;
    }
}

```

#### 92. Reverse Linked List II

- index从1开始算，left和right都是指index

```java
class Solution {
    public ListNode reverseBetween(ListNode head, int left, int right) {
        if (head == null || left == right) {
            return head;
        }

        ListNode dummy = new ListNode(-1); // Create a dummy node to simplify the code.
        dummy.next = head;
        ListNode prev = dummy;

        // Move to the node just before the left position.
        for (int i = 1; i < left; i++) {
            prev = prev.next;
        }

        // Initialize pointers for reversing the sublist.
        ListNode current = prev.next;
        ListNode next = null;

        // Reverse the sublist from left to right.
        for (int i = left; i < right; i++) {
            next = current.next;
            current.next = next.next;
            next.next = prev.next;
            prev.next = next;
        }

        return dummy.next;
    }
}
```

#### 61. Rotate List

- 将链表的尾部与头部相连，形成一个环形链表。
- 计算实际旋转的位置。由于旋转是向右的，所以实际旋转的位置是 len - k % len，其中 len 是链表的长度。这是因为如果k大于链表的长度，旋转k次等于旋转k % len次。
- 找到新的链表头部和尾部。遍历链表，找到原链表的新尾部，它是位于第 len - k % len - 1 个位置的节点，然后新的头部是新尾部的下一个节点。
- 断开环形链表，使其变成一个常规链表。将新尾部的next指针设置为None，同时将原链表的头部指针设置为新头部。
- > Note: 将count初始值设为1，遍历停止条件为 null != node.next 的方式来获取长度并保证 node不为null

```java
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if (null == head || k == 0) {
            return head;
        }

        // 计算链表长度
        int len = 1;
        ListNode node = head;
        while (null != node.next) {
            len++;
            node = node.next;
        }
        
        // 将链表的尾部与头部相连，形成一个环形链表
        node.next = head;

        // 计算实际旋转位置
        k %= len;

        // 找到新的链表头尾
        ListNode new_tail = head;
        for (int i = 0; i < len - k - 1; i++) {
            new_tail = new_tail.next;
        }
        ListNode new_head = new_tail.next;

        // 断开环形链表
        new_tail.next = null;

        return new_head;

    }
}
```

#### 328. Odd Even Linked List
- 需要一个`evenHead`索引到even list的头结点
- 用两个指针odd和even，odd的next先指向even的next，然后odd指针指向自己的next即已经链接上的下一个odd节点。
- 对even做同样处理
- 跳出边界后，将odd.next指向evenHead

```java
class Solution {
    public ListNode oddEvenList(ListNode head) {
        if (null == head || null == head.next || null == head.next.next) {
            return head;
        }

        ListNode odd = head;
        ListNode even = head.next;
        ListNode evenHead = even;

        while (null != even && null != even.next) {
            odd.next = even.next;
            odd = odd.next;
            even.next = odd.next;
            even = even.next;
        }

        odd.next = evenHead;

        return head;

    }
}
```

#### 143. Reorder List
- 快慢指针确定中点middle（选用偶数靠左版本，因为是链表取左操作空间多余右）
- 新建指针second指向middle.next, 然后断开middle与middle.next。second即后半部分。
- 翻转second后半部分-> reversed
- 交错合并head和reversed

> 暂存middle.next节点后断开middle和其next非常重要，否则head开头链表还会带有middle以后得节点（在reverse操作后虽然也会断开，但会使边界判断非常麻烦，先断开再做翻转操作和合并，减少心智负担）

```java
class Solution {
    public void reorderList(ListNode head) {
        

        ListNode fast = head;
        ListNode slow = head;
        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        ListNode middleRight = slow.next;
        slow.next = null;

        ListNode secondReversedHalf = reverseList(middleRight);


        head = mergeAlternately(head, secondReversedHalf);

    }

    private ListNode reverseList(ListNode node) {
        ListNode prev = null;

        while (null != node) {
            ListNode next = node.next;
            node.next = prev;
            prev = node;
            node = next;
        }

        return prev;
    }

    private ListNode mergeAlternately(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode current = dummy;

        while (l1 != null && l2 != null) {
            // Link a node from the first list
            current.next = l1;
            l1 = l1.next;
            current = current.next;

            // Link a node from the second list
            current.next = l2;
            l2 = l2.next;
            current = current.next;
        }

        // If one list is longer than the other, link the remaining nodes
        if (l1 != null) {
            current.next = l1;
        }
        if (l2 != null) {
            current.next = l2;
        }

        return dummy.next;
    }
}
```

### Hash Maps
#### 205. Isomorphic Strings
- 双map映射
- 如果只有单向检查，如"badc"和"baba"就会被认定为true

```java
// 用双Map映射
class Solution {
    public boolean isIsomorphic(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }

        Map<Character, Character> sToTMap = new HashMap<>();
        Map<Character, Character> tToSMap = new HashMap<>();

        for (int i = 0; i < s.length(); i++) {
            char sChar = s.charAt(i);
            char tChar = t.charAt(i);

            if (sToTMap.containsKey(sChar)) {
                if (sToTMap.get(sChar) != tChar) {
                    return false;
                }
            } else {
                sToTMap.put(sChar, tChar);
            }

            if (tToSMap.containsKey(tChar)) {
                if (tToSMap.get(tChar) != sChar) {
                    return false;
                }                
            } else {
                tToSMap.put(tChar, sChar);
            }
        }

        return true;
    }
}
```

- int[] 配合 value计数法
- 维护两个计数：sid，tid，分别代表sc在s中和tc在t中是第几个未映射过的char，如果map[sc] == 0 代表从未出现过的char，计入当前计数并将计数递增
- 判断sc和tc在各自的map中是否都是一样的计数

> note: int[] declare, map数组简化

```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        
        int[] smap = new int[256];
        int[] tmap = new int[256];
        
        int sid = 1;
        int tid = 1;
        
        for (int i = 0; i < s.length(); i++) {
            var sc = s.charAt(i);
            var tc = t.charAt(i);
            
            if (smap[sc] == 0) {
                smap[sc] = sid++;
            }
            if (tmap[tc] == 0) {
                tmap[tc] = tid++;
            }
            
            if (smap[sc] != tmap[tc]) {
                return false;
            }
        }
        
        return true;
    }
}
```

#### 290. Word Pattern

- 与 205. Isomorphic Strings 的计数法相似，只不过有一个arr是String的arr，所以用不了int[]代替map，那个用map就好

> String的split()方法，注意返回值是String的Arr

```java
class Solution {
    public boolean wordPattern(String pattern, String s) {

        String[] sArr = s.split(" ");

        char[] pArr = pattern.toCharArray();

        if (sArr.length != pArr.length) {
            return false;
        }
        
        int[] pmap = new int[256];
        Map<String, Integer> smap = new HashMap<>();
        
        int pid = 1;
        int sid = 1;
        
        for (int i = 0; i < pArr.length; i++) {
            if (pmap[pArr[i]] == 0) {
                pmap[pArr[i]] = pid++;
            }
            
            if (!smap.containsKey(sArr[i])) {
                smap.put(sArr[i], sid++);
            }
            
            if (pmap[pArr[i]] != smap.get(sArr[i])) {
                return false;
            }
        }
        
        return true;
    }
}
```

#### 49. Group Anagrams

- 对于每个字符串，将其字符排序后的结果作为 key，
- 使用hashmap, 将具有相同 key 的字符串放在同一个列表中。

> Arrays.sort()
> new ArrayList<>(map.values()): 用Collection直接初始化一个List(其他Collection 也行，比如Set<String> set = new HashSet<>(someList), 只能将一个list转化为set完成去重)

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        if (strs == null || strs.length == 0) {
            return new ArrayList<>();
        }

        Map<String, List<String>> map = new HashMap<>();

        for (String str : strs) {
            char[] chars = str.toCharArray();

            Arrays.sort(chars);
            String sortedStr = new String(chars);

            List<String> vals = map.getOrDefault(sortedStr, new ArrayList<>());
            vals.add(str);
            map.put(sortedStr, vals);
        }


        return new ArrayList<>(map.values());
    }
}
```


#### 438. Find All Anagrams in a String

- 以p的长度为窗口，在s上滑动遍历
- 用两个哈希表（可简化为int[256]）, 分别表征p的信息和滑动窗口字符串的信息，如果相等就记录当前滑动窗口左边界索引

```java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> result = new ArrayList<>();
        
        if (s == null || s.length() == 0 || p == null || p.length() == 0)
            return result;
        
        // 初始化 p 的字符频率哈希表
        var pArr = p.toCharArray();
        var pMap = new int[256];
        for (char c : pArr) {
            pMap[c]++;
        }
        
        // 初始化滑动窗口的字符频率哈希表
        var sMap = new int[256];        
        // 滑动窗口
        var sArr = s.toCharArray();
        for (int i = 0; i < sArr.length; i++) {
            char currentChar = sArr[i];
            
            // 更新滑动窗口的字符频率
            sMap[currentChar]++;

            // 当窗口大小大于 p.length() 时，移除窗口最左边的字符
            if (i >= pArr.length) {
                char leftChar = sArr[i - pArr.length];
                sMap[leftChar]--;
            }
            
            // 比较哈希表
            if (Arrays.equals(pMap, sMap)) {
                result.add(i - p.length() + 1);
            }
        }
        
        return result;
    }
}
```


#### 974. Subarray Sums Divisible by K
- 前缀和，如果存在三个index的前缀和相同，说明他们两两之间都是符合条件的子数组。也就是算组合数 `C(n, 2) = n! / 2! * (n-2)! = n * (n - 1) / 2`， n是前缀和相同的index数量。
- mod和组合数计算符合条件的子数组数
-  (prefixSum % k + k) % k 可以兼容 prefixSum为负数取模的情况。负数 % k 后一定是一个绝对值小于k的负数，+k再mod，可以起到获得正mod的效果。

```java
class Solution {
    public int subarraysDivByK(int[] nums, int k) {
        // 初始化哈希表，用于记录每个前缀和对 k 取模的次数
        int[] modCount = new int[k];
        // 初始化前缀和
        int prefixSum = 0;
        // 初始化符合条件的子数组个数
        int count = 0;

        // 遍历数组
        for (int num : nums) {
            // 更新前缀和
            prefixSum += num;
            // 更新哈希表
            modCount[(prefixSum % k + k) % k]++;
        }

        // 累加符合条件的子数组个数
        for (int mod : modCount) {
            // 如果某个取模结果的次数大于 1，说明存在至少两个相同的前缀和，可以组成符合条件的子数组
            if (mod > 1) {
                // 计算组合数，n(n-1)/2
                count += mod * (mod - 1) / 2;
            }
        }

        // 加上 modCount[0]，表示前缀和本身就是 k 的倍数的情况
        count += modCount[0];

        return count;
    }
}
```

### Modified Binary Search

#### 278. First Bad Version
- 查找`第一个`等于给定值的元素 类型
```java
public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int left = 0;
        int right = n;

        while (left < right) {
            int mid = left + (right - left) / 2;

            if (isBadVersion(mid)) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }

        return left;
    }
}
```


#### 2529. Maximum Count of Positive Integer and Negative Integer
- 二分法两次找到最后一个小于0的，第一个大于0的(严格)
```java
class Solution {
    public int maximumCount(int[] nums) {
        int len = nums.length;
        
        int low = 0;
        int high = len - 1;
        if (nums[0] > 0 || nums[len - 1] < 0) {
            return len;
        }

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (nums[mid] >= 0) {
                high = mid - 1;
            } else {
                // 当找到最后一个小于target的元素时，继续向左搜索
                low = mid + 1;
            }
        }
        int firstZero = high;

        low = 0;
        high = len - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (nums[mid] <= 0) {
                low = mid + 1;
            } else {
                // 当找到第一个大于target的元素时，继续向左搜索
                high = mid - 1;
            }
        }
        int secondZero = low;

        // 注意一下索引和计数
        return Math.max(firstZero+1, len - 1 - secondZero + 1);        
    }
}
```

#### 33. Search in Rotated Sorted Array
- 确定有序的一侧： 我们首先检查数组的中点。如果中点的值大于等于数组的第一个元素，那么说明中点左侧是有序的。如果中点的值小于数组的第一个元素，那么说明中点右侧是有序的。
- 左侧有序且target落在low-mid间，搜索左侧， 否则搜索右侧
- 右侧有序且target落在mid-high间，搜索右侧，否则搜索左侧

```java
class Solution {
    public int search(int[] nums, int target) {
        int low = 0;
        int high = nums.length - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (nums[mid] == target) {
                return mid;
            }
            if (target == nums[low]) {
                return low;
            }     
            if (target == nums[high]) {
                return high;
            }                         

            if (nums[mid] >= nums[low]) {
                // 左侧有序
                if (target > nums[low] && target < nums[mid]) {
                    high = mid - 1;
                } else {
                    low = mid + 1;
                }
            } else {
                // 右侧有序
                if (target > nums[mid] && target < nums[high]) {
                    low = mid + 1;
                } else {
                    high = mid - 1;
                }
            }
        }

        return -1;
    }
}
```

#### 153. Find Minimum in Rotated Sorted Array
```java
class Solution {
    public int findMin(int[] nums) {
        int len = nums.length;
        int low = 0;
        int high = len - 1;

        // 如果当前范围已经有序，直接返回最小值
        // 处理一开始就是无旋转的升序nums
        if (nums[low] <= nums[high]) {
            return nums[low];
        }        

        while (low <= high) {
            int mid = low + (high - low) / 2;

            // 对应 [2,3,1]这种
            if (mid == len - 1) {
                return nums[mid];
            }

            if (mid > 0 && mid < len - 1 && nums[mid] < nums[mid - 1] && nums[mid] < nums[mid + 1]) {
                return nums[mid];
            }

            // 检查中间元素和右边界的关系，以确定最小值在哪一侧
            if (nums[mid] > nums[high]) {
                // 最小值在mid右侧
                low = mid + 1;
            } else {
                // 在mid左侧或则就是mid
                high = mid - 1;
            }
        }

        return -1;
    }
}
```

#### 162. Find Peak Element
- 二分法
- 可能有多个peak点，所以只需要`mid-1 < mid > mid+1`就可以判断为peak
- 注意index 0 和 len -1的边界判断方式

```java
class Solution {
    public int findPeakElement(int[] nums) {
        int len = nums.length;
        if (len == 1)
            return 0;

        if (nums[0] > nums[1]) 
            return 0;

        if (nums[len-1] > nums[len-2])
            return len-1;

        int begin = 1, end = len-2;

        while (begin <= end) {
            int mid = begin + (end - begin) / 2;

            if (nums[mid] > nums[mid+1] && nums[mid] > nums[mid-1])
                return mid;
            else if (nums[mid] < nums[mid+1])
                begin = mid + 1;
            else if (nums[mid] < nums[mid-1])
                end = mid - 1;  
        }

        return -1;
    }
}
```


### Top K Elements
- 排序和部分排序：快排， 堆（recommend）
- 快选
- 计数排序：适用于元素在一定范围内的情况，统计每个元素的出现次数，然后根据计数结果找出前 k 个元素。时间复杂度为 O(n + k)。

#### 堆
用优先队列获得最大堆和最小堆
- 优先队列（PriorityQueue）默认设置是一个最小堆。在最小堆中，根节点(堆顶)是堆中的最小元素。我们维护一个大小为 k 的最小堆，这样堆顶就是第 k 大的元素
- 要最大堆则需要初始化时指定比较器
```java
Queue<Integer> minHeap = new PriorityQueue<>(k); // k可以设置初始容量

// Comparator.reverseOrder() 是 Java 提供的一个静态方法，用于获取一个逆序的比较器，即最大堆的比较器
Queue<Integer> maxHeap = new PriorityQueue<>(k, Comparator.reverseOrder());
// 或者用Lambda 表达式写比较器
Queue<Integer> maxHeap = new PriorityQueue<>(k, (a, b) -> b - a);
```


#### 703. Kth Largest Element in a Stream
- 用一个最小堆来记录第k大
```java
class KthLargest {

    Queue<Integer> minHeap;
    int k;

    public KthLargest(int k, int[] nums) {
        this.k = k;
        this.minHeap = new PriorityQueue<>(k);

        for (int num : nums) {
            add(num);
        }
    }

    public int add(int val) {
        minHeap.offer(val);
        
        if (minHeap.size() > k) {
            minHeap.poll();
        }
        
        return minHeap.peek();
    }
}
```

#### 215. Kth Largest Element in an Array
- 最小堆
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        
        PriorityQueue<Integer> queue = new PriorityQueue<>(k);
        
        for (int num : nums) {
            queue.offer(num);
            
            if (queue.size() > k) {
                queue.poll();
            }
        }
        
        return queue.peek();
    }
}
```

- 快选
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        return quickSelect(nums, 0, nums.length - 1, k);
    }

    private int quickSelect(int[] nums, int left, int right, int k) {
        while (left <= right) {
            int pivotIndex = randomPartition(nums, left, right);

            if (pivotIndex == k - 1) {
                return nums[pivotIndex];
            } else if (pivotIndex > k - 1) {
                right = pivotIndex - 1;
            } else {
                left = pivotIndex + 1;
            }
        }

        return -1; // 这里表示没有找到，具体可以根据实际情况返回合适的值
    }

    private int randomPartition(int[] nums, int left, int right) {
        int randomIndex = left + new Random().nextInt(right - left + 1);
        swap(nums, randomIndex, right);

        int pivot = nums[right];
        int i = left - 1;

        for (int j = left; j < right; j++) {
            if (nums[j] >= pivot) {
                i++;
                swap(nums, i, j);
            }
        }

        swap(nums, i + 1, right);

        return i + 1;
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }

}
```

- 快排
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        int len = nums.length;
        quickSort(nums, 0, len - 1);
        return nums[len-k];
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }

    private void quickSort(int[] arr, int low, int high) {
        if(low >= high) {
            return ;
        }

        int i = low, j = high;
        
        while(i < j) {
            while(i < j && arr[j] >= arr[low]) {
            j--;
            }

            while(i < j && arr[i] <= arr[low]) {
            i++;
            }

            swap(arr, i, j);
        }

        swap(arr, low, i);

        quickSort(arr, low, i - 1);
        quickSort(arr, i + 1, high);
    }
}
```

#### 973. K Closest Points to Origin
- 本质还是经典TOP K，可以大根堆，快选，快排
- 用大根堆，可以直接重写比较器比较平方和


```java
// 大根堆变种
class Solution {
    public int[][] kClosest(int[][] points, int k) {
        var maxHeap = new PriorityQueue<int[]>(
            (a, b) -> (b[0]*b[0] + b[1]*b[1]) - (a[0]*a[0] + a[1]*a[1])
        );

        for (int[] point : points) {
            maxHeap.offer(point);
            if (maxHeap.size() > k) {
                maxHeap.poll();
            }
        }

        int[][] result = new int[k][2];
        while (k-- > 0) {
            result[k] = maxHeap.poll();
        }

        return result;
    }
}
```


#### 347. Top K Frequent Elements
- 用哈希表记录key和出现频次，然后用大根堆遍历存储map的entry。
- 重写比较器比较entry的value
- 另外一种主流解法是`桶排序`，见第二个snippet

> 关于桶排序： 基本思想是将数组划分为若干个桶，每个桶代表一定范围的数值。然后对每个桶中的元素进行排序，最后按照桶的顺序将各个桶中的元素合并起来。


```java
// 大根堆变种
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        var map = new HashMap<Integer, Integer>();

        for (int i : nums)
            map.put(i, map.getOrDefault(i, 0) + 1);

        var maxHeap = new PriorityQueue<Map.Entry<Integer, Integer>>(
            (a, b) -> (a.getValue() - b.getValue())
        );

        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            maxHeap.offer(entry);
            if (maxHeap.size() > k)
                maxHeap.poll();
        }

        int[] result = new int[k];
        while (k-- > 0)
            result[k] = maxHeap.poll().getKey();

        return result;
    }
}
```

对于TOP k frequent这类问题，桶排序的思路可以用在统计元素频率上。
- 统计频率并放入桶中： 使用哈希表统计每个元素的频率。然后，根据频率将元素放入对应的桶中。
- 从高频到低频遍历桶： 从频率最高的桶开始遍历，依次取出桶中的元素。当取出的元素个数达到k时，就得到了前k个高频元素。

```java
// 桶排序
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        // Step 1: 统计每个元素的频率
        var frequencyMap = new HashMap<Integer, Integer>();
        for (int num : nums) {
            frequencyMap.put(num, frequencyMap.getOrDefault(num, 0) + 1);
        }

        // Step 2: 使用桶排序，buckets[i] 存放频率为 i 的元素列表
        int n = nums.length;
        ArrayList<Integer>[] buckets = new ArrayList[n + 1];

        for (int i = 0; i <= n; i++) {
            buckets[i] = new ArrayList<>();
        }

        for (Map.Entry<Integer, Integer> entry : frequencyMap.entrySet()) {
            int num = entry.getKey();
            int freq = entry.getValue();
            buckets[freq].add(num);
        }

        // Step 3: 从桶的末尾开始，将元素加入结果数组，直到结果数组的长度达到 k
        int[] result = new int[k];
        int idx = 0;

        for (int i = n; i > 0 && idx < k; i--) {
            if (!buckets[i].isEmpty()) {
                for (int num : buckets[i]) {
                    result[idx++] = num;
                    if (idx == k) {
                        break;
                    }
                }
            }
        }

        return result;
    }
}
```

#### 358. Rearrange String k Distance Apart
Given a non-empty string str and an integer k, rearrange the string such that the same characters are at least distance k from each other.

All input strings are given in lowercase letters. If it is not possible to rearrange the string, return an empty string "".

给定一个非空字符串和一个整数k，重新排列该字符串，使相同的字符彼此之间至少有k个距离。

所有输入字符串都以小写字母表示。

如果无法重新排列字符串，则返回空字符串“”。

```txt
Example 1:

str = " ", k = 3

Result: "abcabc"
The same letters are at least distance 3 from each other.
```

---
- 贪心算法和大根堆
- int[] 存储char和出现次数
- 大根堆，堆顶是出现频率最高的字符
- 构建结果字符串： 从堆中取出字符，将其放入结果字符串。
- 为了确保相同字符的距离至少为k，你可以使用一个队列来存储最近放入结果字符串的字符。
  - 对每个堆顶弹出的char，在append到stringBuilder后，将其frequency减1，然后将更新后的entry加入一个队列。
  - 当这个队列的size达到k时，说明距离队首元素加入stringBuilder后已经有k-1个不同的char加入stringBuilder，此时将队首entry出队重新加入堆，如果其freq足够高仍然能处在堆顶，在下一次出堆时就能保证和上一次之间的距离为K

```java

class Solution {

    public static String rearrangeString(String str, int k) {
        if (k <= 1) {
            return str;
        }

        // 统计字符频率
        Map<Character, Integer> charFreq = new HashMap<>();
        for (char c : str.toCharArray()) {
            charFreq.put(c, charFreq.getOrDefault(c, 0) + 1);
        }

        // 创建最大堆
        PriorityQueue<Map.Entry<Character, Integer>> maxHeap = new PriorityQueue<>(
                (a, b) -> Integer.compare(b.getValue(), a.getValue())
        );
        maxHeap.addAll(charFreq.entrySet());

        // 构建结果字符串
        StringBuilder result = new StringBuilder();
        Queue<Map.Entry<Character, Integer>> queue = new LinkedList<>();

        while (!maxHeap.isEmpty()) {
            Map.Entry<Character, Integer> entry = maxHeap.poll();
            char character = entry.getKey();
            int frequency = entry.getValue();

            // 将字符加入结果字符串
            result.append(character);

            // 将字符及其频率放入队列，以便之后检查距离
            queue.offer(new AbstractMap.SimpleEntry<>(character, frequency - 1));

            if (queue.size() == k) {
                // 检查队列头部的字符是否已经满足距离要求
                Map.Entry<Character, Integer> front = queue.poll();
                if (front.getValue() > 0) {
                    maxHeap.offer(front);
                }
            }
        }

        return result.length() == str.length() ? result.toString() : "";
    }
}

```


### Sliding Window
#### 239. Sliding Window Maximum
- 单调递减队列， 队首保持当前窗口最大值
- 注意窗口初次形成时记录第一个值
- 处理后续元素时注意窗口最左的脚标

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if(nums.length == 0 || k == 0){
            return new int[]{};
        }
        Deque<Integer> monoQueue = new ArrayDeque<>();
        int[] res = new int[nums.length - k + 1];

        // 处理前 k 个元素
        for(int i = 0; i < k; i++){
            // 将单调队列中比nums[i]小的都弹出
            while(!monoQueue.isEmpty() && monoQueue.peekLast() < nums[i]){
                monoQueue.pollLast();
            }
            // 队尾压入nums[i], 此时队列仍是单调，队尾最小
            monoQueue.offerLast(nums[i]);
        }

        // 初始化结果数组中的第一个元素，即窗口首次形成时的最大值。
        // 第一个循环中，处理了数组的前 k 个元素, 此时队首元素就是这个窗口中的最大值
        res[0] = monoQueue.peekFirst();

        // 处理剩余元素, k 开始遍历到数组末尾。
        for(int i = k; i < nums.length; i++){
            // 注意是i-k,即此次从左边移出窗口的num
            // 如果队首元素是窗口最左边的元素（即要移出窗口的元素），则将其移出队列。
            if(monoQueue.peekFirst() == nums[i-k]){
                monoQueue.pollFirst();
            }
            // 类似的保证单调递减队列并遍历后续元素
            while(!monoQueue.isEmpty() && monoQueue.peekLast() < nums[i]){
                monoQueue.pollLast();
            }
            monoQueue.offerLast(nums[i]);
            // 将队列的队首元素（即当前窗口的最大值）存入结果数组。
            res[i-k+1] = monoQueue.peekFirst();
        }

        return res;
    }
}
```

#### 480. Sliding Window Median
`median` 是有序整数列表中的中间值。
如果列表的大小为偶数，则没有中间值。所以中位数就是这两个中间值的平均值。

给你一个整数数组数字和一个整数k。
有一个大小为k的滑动窗口，它从数组的最左边移动到最右边。
你只能在窗口中看到k个数字。
每次滑动窗口向右移动一个位置。

返回原始数组中每个窗口的`median` 的array。在实际值的10-5以内的答案将被接受。

--- 

- 双堆获取中位数

```java
class Solution {
    public double[] medianSlidingWindow(int[] nums, int k) {
        var maxHeap = new PriorityQueue<Integer>(Collections.reverseOrder());
        var minHeap = new PriorityQueue<Integer>();
        List<Double> result = new ArrayList<>();


        for (int i = 0; i < nums.length; i++) {
            if (!maxHeap.isEmpty() && nums[i] <= maxHeap.peek()) {
                maxHeap.offer(nums[i]);
            } else {
                minHeap.offer(nums[i]);
            }

            // Balance the heaps
            while (maxHeap.size() > (k + 1) / 2) {
                minHeap.offer(maxHeap.poll());
            }

            while (minHeap.size() > k / 2) {
                maxHeap.offer(minHeap.poll());
            }

            // Calculate and add the median to the result
            if (i >= k - 1) {
                double median;
                if (k % 2 == 0) {
                    median = ((double)maxHeap.peek() + (double)minHeap.peek()) / 2.0;
                } else {
                    median = (double) maxHeap.peek();
                }
                result.add(median);

                // Remove the element that is out of the window
                int removed = nums[i - k + 1];
                if (removed <= maxHeap.peek()) {
                    maxHeap.remove(removed);
                } else {
                    minHeap.remove(removed);
                }
            }
        }

        return result.stream().mapToDouble(Double::doubleValue).toArray();
    }
}
```


### Two Heaps
#### 1985. Find the Kth Largest Integer in the Array
- 最小堆
- 比较器和int版本不一样，也不能直接parseInt相减，因为可能会超出int范围
```java
class Solution {
    public String kthLargestNumber(String[] nums, int k) {
        PriorityQueue<String> minHeap = new PriorityQueue<>((a, b) -> {
            if (a.length() != b.length()) {
                return a.length() - b.length(); // 按长度升序
            }
            return a.compareTo(b); // 长度相等时按照字符串大小升序
        });

        // 或者
        PriorityQueue<String> minHeap = new PriorityQueue<>(Comparator.comparingInt(String::length).thenComparing(Comparator.naturalOrder()));
        
        for (String str : nums) {
            minHeap.offer(str);
            
            if (minHeap.size() > k) {
                minHeap.poll();
            }
        }
        
        return minHeap.peek();        
    }
}
```

#### 4. Median of Two Sorted Arrays
```java
// Two Heap解法
public class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Comparator.reverseOrder());
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        
        for (int num : nums1) {
            maxHeap.offer(num);
            minHeap.offer(maxHeap.poll());
            if (maxHeap.size() < minHeap.size()) {
                maxHeap.offer(minHeap.poll());
            }
        }
        
        for (int num : nums2) {
            maxHeap.offer(num);
            minHeap.offer(maxHeap.poll());
            if (maxHeap.size() < minHeap.size()) {
                maxHeap.offer(minHeap.poll());
            }
        }
        
        if (maxHeap.size() == minHeap.size()) {
            return (double) (maxHeap.peek() + minHeap.peek()) / 2;
        } else {
            return maxHeap.peek();
        }
    }
}
```

采用二分查找的思路，并且时间复杂度为 O(log(min(m, n))) 的解法：

1. 确保 nums1 是较小的数组：
如果 nums1 的长度大于 nums2，则交换它们。这并不是算法的必需步骤，但它简化了实现。

2. 在较小的数组上进行二分查找：
在较小的数组 nums1 上执行二分查找。基本思想是对两个数组进行划分，使得划分点左边的元素都小于右边的元素。

3. 计算中位数：
一旦找到正确的划分点，可以根据划分点处的元素计算中位数。

4. 调整划分点：
如果两个数组中元素的总数是偶数，需要考虑划分点周围的两个元素来计算中位数。

```java
public double findMedianSortedArrays(int[] nums1, int[] nums2) {
    // 确保 nums1 是较小的数组。
    if (nums1.length > nums2.length) {
        int[] temp = nums1;
        nums1 = nums2;
        nums2 = temp;
    }

    int x = nums1.length;
    int y = nums2.length;
    int low = 0;
    int high = x;

    while (low <= high) {
        int partitionX = (low + high) / 2;
        int partitionY = (x + y + 1) / 2 - partitionX;

        int maxX = (partitionX == 0) ? Integer.MIN_VALUE : nums1[partitionX - 1];
        int minX = (partitionX == x) ? Integer.MAX_VALUE : nums1[partitionX];

        int maxY = (partitionY == 0) ? Integer.MIN_VALUE : nums2[partitionY - 1];
        int minY = (partitionY == y) ? Integer.MAX_VALUE : nums2[partitionY];

        if (maxX <= minY && maxY <= minX) {
            // 找到了正确的划分点。
            if ((x + y) % 2 == 0) {
                // 元素总数为偶数，返回中间两个元素的平均值。
                return (Math.max(maxX, maxY) + Math.min(minX, minY)) / 2.0;
            } else {
                // 元素总数为奇数，返回中间两个元素中的较大值。
                return Math.max(maxX, maxY);
            }
        } else if (maxX > minY) {
            // 需要将划分点在 nums1 中左移。
            high = partitionX - 1;
        } else {
            // 需要将划分点在 nums1 中右移。
            low = partitionX + 1;
        }
    }

    // 如果执行到这里，表示数组没有被正确排序。
    throw new IllegalArgumentException("输入数组未排序。");
}

```


#### 378. Kth Smallest Element in a Sorted Matrix
给定一个`n x n`矩阵，其中每行和每列都按升序排序，则返回矩阵中第k个最小的元素。

请注意，它是排序顺序中第k个最小的元素，而不是第k个不同的元素。

您必须找到内存复杂度优于O(N2)的解决方案。

---
##### 大根堆

```java
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        if (null == matrix || null == matrix[0])
            return -1;

        int rowLen = matrix.length;
        int colLen = matrix[0].length;

        if (rowLen == 0 || colLen == 0)
            return -1;

        var maxHeap = new PriorityQueue<Integer>(
            (a, b) -> (b - a)
        );

        for (int i = 0; i < rowLen; i++) {
            for (int j = 0; j < colLen; j++) {
                maxHeap.offer(matrix[i][j]);

                if (maxHeap.size() > k) {
                    maxHeap.poll();
                }
            }
        }

        return maxHeap.peek();
    }
}
```

##### 二分搜索（最优性能）
说实话，没法理解为什么更新low=mid+1，high = mid，mid都不一定在矩阵中。
```java
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int n = matrix.length;
        int low = matrix[0][0];
        int high = matrix[n - 1][n - 1];

        while (low < high) {
            int mid = low + (high - low) / 2;
            int count = countLessEqual(matrix, mid);

            if (count < k) {
                low = mid + 1;
            } else {
                high = mid;
            }
        }

        return low;
    }

    private int countLessEqual(int[][] matrix, int target) {
        int n = matrix.length;
        int count = 0;
        int row = n - 1;
        int col = 0;

        while (row >= 0 && col < n) {
            if (matrix[row][col] <= target) {
                count += row + 1;
                col++;
            } else {
                row--;
            }
        }

        return count;
    }

}
```

### K-way merge

### Backtracking

#### 78. Subsets
给定一个包含 ***唯一元素*** 的整数数组nums，返回所有可能的子集

解决方案集不能包含重复的子集。以任何顺序返回解决方案。

```txt
Example 1:

Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```
---

- 回溯法（backtracking）
- 递归回溯法： 对于每个元素，你有两个选择，要么包含它，要么不包含它。通过递归，你可以生成所有的组合。
- 回溯过程： 在递归的每一步，你需要记录当前的组合。当遍历到数组的末尾时，将当前的组合加入结果集。

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        generateSubsets(nums, 0, new ArrayList<>(), result);
        return result;
    }

    private void generateSubsets(
        int[] nums, 
        int index, 
        List<Integer> current, 
        List<List<Integer>> result
    ) {
        // 添加当前组合到结果集
        result.add(new ArrayList<>(current));

        // 从当前位置向后遍历数组
        for (int i = index; i < nums.length; i++) {
            // 选择当前元素
            current.add(nums[i]);
            // 递归生成子集
            generateSubsets(nums, i + 1, current, result);
            // 回溯，移除当前元素
            current.remove(current.size() - 1);
        }
    }
}
```
#### 90. Subsets II
给定一个`可能包含重复项`的整数数组nums，返回所有可能得子集

解决方案集不能包含重复的子集。以任何顺序返回解决方案。
```txt
Example 1:

Input: nums = [1,2,2]
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]
```

---

- 和subsets的差异在于 可能包含重复项
- 排序数组，方便后面进行跳过
- 跳过重复： 在递归的过程中，如果当前元素和前一个元素相同，就跳过这个元素，避免重复生成相同的子集。

举例[1,1,2] 中 遍历时，只有index=0的1会执行递归回溯
```txt
如果没有跳过代码，会得到：
[[],[1],[1,2],[1,2,2],[1,2],[2],[2,2],[2]]

实际上需要的效果是：
[[],[1],[1,2],[1,2,2],[2],[2,2]]

可见，不跳过的话第二个1会生成重复的[1,2],[2]
```


```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        // 排序数组，方便后面进行跳过
        Arrays.sort(nums);
        backtrack(nums, 0, new ArrayList<>(), result);
        return result;
    }

    private void backtrack(
        int[] nums, 
        int start, 
        List<Integer> current, 
        List<List<Integer>> result
    ) {
        // 添加当前子集到结果集
        result.add(new ArrayList<>(current));

        // 递归生成子集
        for (int i = start; i < nums.length; i++) {
            // 跳过重复元素
            if (i > start && nums[i] == nums[i - 1]) {
                continue;
            }
            current.add(nums[i]);
            backtrack(nums, i + 1, current, result);
            current.remove(current.size() - 1);
        }
    }
}
```


#### 39. Combination Sum
给定一个 ***不同*** 的整数候选数组和一个目标整数目标，返回所选数字与目标之和的所有唯一候选组合的列表。
您可以按任何顺序退回这些组合。

可以从候选人中选择相同的数字，次数不限。
两个组合是唯一的，如果至少有一个被选取的number的频率不一样

生成测试用例，使得对于给定输入，合计到目标的唯一组合的数量少于150个组合。

```txt
Example 1:

Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
Explanation:
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.
```

---

- 回溯
- 判断添加到res的条件与target相关
- 在循环回溯的时候，传入的index不需要+1，因为本题运行重复选取统一个元素

```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(candidates);
        backtrack(candidates, 0, target, new ArrayList<>(), result);
        return result;
    }

    private void backtrack(
        int[] candidates,
        int index,
        int remaining,
        List<Integer> current,
        List<List<Integer>> result
    ) {
        if (remaining == 0) {
            result.add(new ArrayList(current));
            return;
        }

        for (int i = index; i < candidates.length; i++) {
            // 剪枝，如果当前元素已经大于目标，后面的元素更大，就不可能满足条件，直接跳过
            // Note：比进入新一个递归后判断remaining是否小于0再return好，
            // 这个能跳过后面比当前元素大的所用元素，前者还是会递归这些元素然后在开头return，不如直接break
            if (candidates[i] > remaining) {
                break;
            }

            current.add(candidates[i]);
            // Note：这里传递的index还是i，这样才使重复选取一个ele成为可能。
            backtrack(candidates, i, remaining - candidates[i], current, result);
            current.remove(current.size()-1);
        }
    }
}
```

#### 40. Combination Sum II
给出一个候选号(候选者)和一个目标号(目标)的集合，在候选者中找到候选者中所有唯一的组合，其中候选者数字之和为目标。

***考生名单中的每个数字只能在组合中使用一次。***

注意：解决方案集不能包含重复的组合。

```txt
Example 1:

Input: candidates = [10,1,2,7,6,1,5], target = 8
Output: 
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]
```

---

- 回溯
- 不能包含重复的组合： 排序并跳过
- 每个数字只能在组合中使用一次： 递归调用更新index时递增1

```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(candidates); // 排序是为了后面方便去重

        backtrack(result, new ArrayList<>(), candidates, target, 0);

        return result;                
    }

    private void backtrack(
        List<List<Integer>> result, 
        List<Integer> current, 
        int[] candidates, 
        int remaining, 
        int start
    ) {
        if (remaining == 0) {
            // 如果目标为0，说明找到了一个符合条件的组合
            result.add(new ArrayList<>(current));
            return;
        }

        for (int i = start; i < candidates.length; i++) {
            // 避免重复，如果当前元素和上一个相同，跳过
            if (i > start && candidates[i] == candidates[i - 1]) {
                continue;
            }

            // 剪枝，如果当前元素已经大于目标，后面的元素更大，就不可能满足条件，直接跳过
            if (candidates[i] > remaining) {
                break;
            }

            // 尝试将当前元素加入组合
            current.add(candidates[i]);

            // 递归调用，更新目标值和起始位置
            backtrack(result, current, candidates, remaining - candidates[i], i + 1);

            // 回溯，撤销选择，继续尝试其他组合
            current.remove(current.size() - 1);
        }
    }    
}
```

#### 113. Path Sum II

> 给定一个二叉树的根和一个整数`targetSum`，返回路径中节点值之和等于`targetSum`的所有`根到叶路径`。
> 
> 每条路径都应该作为节点值列表返回，而不是节点引用。
> 
> 根到叶路径是从根开始并在任何叶节点结束的路径。叶子是没有子节点的节点。

```txt
Input: root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22

Output: [[5,4,11,2],[5,8,4,5]]

Explanation: There are two paths whose sum equals targetSum:
5 + 4 + 11 + 2 = 22
5 + 8 + 4 + 5 = 22
```

---
- 回溯
- 当到达叶子节点且路径和等于目标值时，添加路径的副本
  - 因为是叶子结点所以要判断左右子节点为null
  - 如果找到，


```java
class Solution {

    List<List<Integer>> result;
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        result = new ArrayList<>();

        backtrack(root, targetSum, new ArrayList<Integer>());

        return result;

    }

    private void backtrack(TreeNode node, int remaining, List<Integer> current){

        if (node == null) {
            return;
        }

        int newRemaining = remaining - node.val;

        current.add(node.val);

        if (node.left == null && node.right == null && newRemaining == 0) {
            result.add(new ArrayList(current));
            // 因为这里是guide语句，所以要在return之前将状态回滚
            // 如果将下方两个backtrack写入else，则可以共用最后的回滚语句
            current.remove(current.size()-1);
            return;
        }

        backtrack(node.left, newRemaining, current);
        backtrack(node.right, newRemaining, current);
        current.remove(current.size()-1);
    }
}
```


#### 131. Palindrome Partitioning
给定一串S，划分S，使划分出的每一个子串是回文。
返回S的所有可能的回文划分。

```txt
Example 1:

Input: s = "aab"
Output: [["a","a","b"],["aa","b"]]
```
---

- 回溯
- 添加到结果并退出的条件是index到s最后一位
- 循环时用的index是end，且考虑到substring的前闭后开特性，停止条件是 <= 而非 <
- 递归时index需要更新到end，而不是递增一位

```java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> result = new ArrayList<>();
        backtrack(result, new ArrayList<>(), s, 0);
        return result;
    }

    private void backtrack(
        List<List<String>> result, 
        List<String> current, 
        String s, 
        int start
    ) {
        if (start == s.length()) {
            result.add(new ArrayList(current));
            return;
        }

        // Note： 遍历i为end，结束条件是<=, 考虑到substring的截取方式是前闭后开的
        for (int end = start+1; end <= s.length(); end++) {
            if (isPalindrome(s, start, end-1)) {
                current.add(s.substring(start, end));
                // Note: 此处更新index为end，跳过了被添加的回文区域
                backtrack(result, current, s, end);
                current.remove(current.size()-1);
            }
        }
    }

    private boolean isPalindrome(String s, int low, int high) {
        while (low < high) {
            if (s.charAt(low++) != s.charAt(high--)) {
                return false;
            }
        }
        return true;
    }    
}
```

#### 22. Generate Parentheses
在给定n对圆括号的情况下，编写一个函数来生成格式良好的圆括号的所有组合。

```txt
Example 1:

Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]
```

--- 
- 回溯获得全部组合
- 用open，close记录当前current使用开闭括号数量
- 添加到结果并return的条件式长度达到2n
- well formed判断
  - 左括号数量小于n
  - 右括号数量小于左括号数量

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();
        backtrack(result, new StringBuilder(), 0, 0, n);
        return result;        
    }

    private void backtrack(
        List<String> result, 
        StringBuilder current, 
        int open, 
        int close, 
        int max
    ) {
        // 如果当前字符串的长度等于2 * n，表示找到一个合法的组合        
        if (current.length() == 2*max) {
            result.add(new String(current));
            return;
        } 

        // 如果左括号数量小于 n，可以添加左括号
        if (open < max) {
            current.append('(');
            backtrack(result, current, open + 1, close, max);
            current.deleteCharAt(current.length()-1);
        }

        // 如果右括号数量小于左括号数量，可以添加右括号
        if (close < open) {
            current.append(')');
            backtrack(result, current, open, close + 1, max);
            current.deleteCharAt(current.length()-1);            
        }
    }
}
```

#### 17. Letter Combinations of a Phone Number
给定一个包含2-9（包括2和9）数字的字符串，返回该数字可能表示的所有可能的字母组合。
按任意顺序返回答案。

下面给出了数字到字母的映射（就像电话按键一样）。请注意，1不映射到任何字母。
```txt
1 - null
2 - abc
3 - def
4 - ghi
5 - jkl
6 - mno
7 - pqrs
8 - tuv
9 - wxyz
```
---

- 递归回溯法

```java
class Solution {

    private static final Map<Character, char[]> digitMap = new HashMap<>();

    static {
        digitMap.put('2', new char[]{'a', 'b', 'c'});
        digitMap.put('3', new char[]{'d', 'e', 'f'});
        digitMap.put('4', new char[]{'g', 'h', 'i'});
        digitMap.put('5', new char[]{'j', 'k', 'l'});
        digitMap.put('6', new char[]{'m', 'n', 'o'});
        digitMap.put('7', new char[]{'p', 'q', 'r', 's'});
        digitMap.put('8', new char[]{'t', 'u', 'v'});
        digitMap.put('9', new char[]{'w', 'x', 'y', 'z'});
    }

    public List<String> letterCombinations(String digits) {

        List<String> result = new ArrayList<>();

        if (null == digits || digits.length() == 0)
            return result;

        backtrack(new StringBuilder(), digits, result);

        return result;
    }

    private void backtrack(
        StringBuilder combination, 
        String nextDigits, 
        List<String> result
    ) {
        // 如果没有下一个数字了，说明当前组合已经完成
        if (nextDigits.length() == 0) {
            result.add(combination.toString());
            return;
        }
        // 获取当前数字对应的字母数组
        char digit = nextDigits.charAt(0);
        char[] letters = digitMap.get(digit);        

        // 遍历字母数组，递归调用
        for (char letter : letters) {
            combination.append(letter);

            /*
            nextDigits.substring(1) 表示取 nextDigits 字符串的子字符串，从索引 1 开始一直到字符串的末尾。这是因为字符串的索引是从 0 开始的。

            举个例子，如果 nextDigits 是 "234"，那么 nextDigits.substring(1) 就是 "34"。这是一个常见的操作，用来在递归中去掉当前处理的数字，以便处理下一个数字。
            */
            backtrack(combination, nextDigits.substring(1), result);
            
            // 回溯，移除最后一个字符
            combination.deleteCharAt(combination.length() - 1); 
        }
    }
}
```

对于 nextDigits 的处理，目前的实现在每次递归调用中使用 nextDigits.substring(1) 来获取剩余的数字串。这是一种比较简单的方式，但在处理大量数据时可能会有性能开销。

一种优化的方式是不使用 substring，而是传递当前处理的位置索引。这样可以减少创建字符串对象的开销。

```java
// 采用传index的版本
class Solution {

    private static final Map<Character, char[]> digitMap = new HashMap<>();

    static {
        digitMap.put('2', new char[]{'a', 'b', 'c'});
        digitMap.put('3', new char[]{'d', 'e', 'f'});
        digitMap.put('4', new char[]{'g', 'h', 'i'});
        digitMap.put('5', new char[]{'j', 'k', 'l'});
        digitMap.put('6', new char[]{'m', 'n', 'o'});
        digitMap.put('7', new char[]{'p', 'q', 'r', 's'});
        digitMap.put('8', new char[]{'t', 'u', 'v'});
        digitMap.put('9', new char[]{'w', 'x', 'y', 'z'});
    }

    public List<String> letterCombinations(String digits) {

        List<String> result = new ArrayList<>();

        if (null == digits || digits.length() == 0)
            return result;

        // index和digits代替nextDigits
        backtrack(new StringBuilder(), digits.toCharArray(), 0, result);

        return result;
    }

    private void backtrack(
        StringBuilder combination, 
        char[] digits,
        int index,
        List<String> result
    ) {
        // 如果当前索引越界，说明当前组合已经完成
        if (index == digits.length) {
            result.add(combination.toString());
            return;
        }
        
        // 获取当前数字对应的字母数组
        char digit = digits[index];
        char[] letters = digitMap.get(digit);        

        // 遍历字母数组，递归调用
        for (char letter : letters) {
            combination.append(letter);

            backtrack(combination, digits, index + 1, result);
            
            // 回溯，移除最后一个字符
            combination.deleteCharAt(combination.length() - 1); 
        }
    }
}
```


#### 1079. Letter Tile Possibilities
您有n个瓷砖，每个瓷砖上印有一个字母瓷砖[i]。

返回您可以使用这些瓷砖上打印的字母组成的可能的非空字母序列的数量。

```txt
Example 1:

Input: tiles = "AAB"
Output: 8
Explanation: The possible sequences are "A", "B", "AA", "AB", "BA", "AAB", "ABA", "BAA".
```

---

- 回溯
- 跳过重复的判断要考虑前一个char是否也未被使用

```java
class Solution {

    int ans;            // 记录最终的答案
    boolean[] visited;  // 记录字符是否已经被访问过

    public int numTilePossibilities(String tiles) {
        char[] arr = tiles.toCharArray();
        Arrays.sort(arr);   // 将字符数组排序，以便处理相同字符的重复情况

        visited = new boolean[arr.length];

        backtrack(arr, 0);  // 开始深度优先搜索

        return ans;
    }

    private void backtrack(char[] arr, int len) {
        if (len == arr.length)
            return;

        for (int i = 0; i < arr.length; i++) {
            if (visited[i])
                continue;
            if (i > 0 && arr[i] == arr[i - 1] && !visited[i - 1])
                continue;  // 处理相同字符的情况，避免重复

            ans++;  // 每次选择一个字符，答案加一

            visited[i] = true;    // 标记当前字符已被访问
            backtrack(arr, len + 1);    // 递归调用深度优先搜索
            visited[i] = false;   // 回溯，取消当前字符的访问标记
        }
    }
}
```

#### 79. Word Search
> 给定一个`m x n`网格的字符板和一个字符串单词，如果网格中存在单词，则返回TRUE。
> 
> 该单词可以由连续相邻单元格的字母构成，其中相邻单元格水平或垂直相邻。同一字母单元不能多次使用。

```txt
Input: 
board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"

Output: true
```

---

- 回溯
- 主方法里需要遍历每个grid调用backtrack，因为每一个grid都可以作为开头
- 可选优化1：统计char freq，筛除不够组成word的board
- 可选优化2：翻转wordArray，如果尾字符频率高于首字符频率

```java
class Solution {

    boolean[][] used;

    public boolean exist(char[][] board, String word) {

        int rows = board.length; 
        int cols = board[0].length;

        used = new boolean[rows][cols];
        char[] wordArr = word.toCharArray();

        // 统计字符在board中的出现次数
        int[] boardCharFrequency = new int[52];
        for (int i = 0; i < rows; ++i) {
            for (int j = 0; j < cols; ++j) {
                ++boardCharFrequency[board[i][j]];
            }
        }

        // 检查单词字符是否超过在board中的出现次数
        for (char ch : wordArray) {
            if (--boardCharFrequency[ch] < 0) {
                return false;
            }
        }

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (backtrack(board, wordArr, 0, i, j))
                    return true; 
            }
        }

        return false;
    }

    private boolean backtrack(
        char[][] board,
        char[] wordArr,
        int index,
        int x,
        int y
    ) {
        if (!withinBoundary(board, x, y)) {
            return false;
        }

        if (used[x][y]) {
            return false;
        }

        if (board[x][y] != wordArr[index]) {
            return false;
        }

        if (index == wordArr.length-1) {
            return true;
        }

        used[x][y] = true;
        if (backtrack(board, wordArr, index+1, x+1, y) 
            || backtrack(board, wordArr, index+1, x-1, y)
            || backtrack(board, wordArr, index+1, x, y+1)
            || backtrack(board, wordArr, index+1, x, y-1)
        )
            return true;

        used[x][y] = false;
        return false;
    }

    private boolean withinBoundary(char[][] board, int x, int y) {
        return x >= 0 
            && x < board.length 
            && y >= 0
            && y < board[0].length;
    }
}
```






### Greedy
#### 455. Assign Cookies
- 对孩子的贪心因子数组 g 和饼干的大小数组 s 进行排序
- 使用两个指针，一个指向孩子数组 g，另一个指向饼干数组 s。从最小的贪心因子和最小的饼干尺寸开始，逐个比较。
  - 如果 s[j] >= g[i]，表示当前饼干可以满足当前孩子，将两者都移向下一个。
  - 如果 s[j] < g[i]，表示当前饼干不足以满足当前孩子，需要尝试更大的饼干，将饼干指针向后移动。

```java
public class CookieProblem {
    public int findContentChildren(int[] g, int[] s) {
        Arrays.sort(g);
        Arrays.sort(s);
        
        int i = 0; // 孩子数组的指针
        int j = 0; // 饼干数组的指针
        int count = 0; // 记录满足的孩子数
        
        while (i < g.length && j < s.length) {
            if (s[j] >= g[i]) {
                count++;
                i++;
            }
            j++;
        }
        
        return count;
    }
}

```


### DFS

#### 1079. Letter Tile Possibilities
您有n个瓷砖，每个瓷砖上印有一个字母瓷砖[i]。

返回您可以使用这些瓷砖上打印的字母组成的可能的非空字母序列的数量。

```txt
Example 1:

Input: tiles = "AAB"
Output: 8
Explanation: The possible sequences are "A", "B", "AA", "AB", "BA", "AAB", "ABA", "BAA".
```

---

- DFS

```java
class Solution {
    public int numTilePossibilities(String tiles) {
        // 记录每个字母的出现次数
        int[] letterCount = new int[26];
        for (char c : tiles.toCharArray()) {
            letterCount[c - 'A']++;
        }

        // 从第一个字母开始深度优先搜索
        return dfs(letterCount);
    }

    private int dfs(int[] letterCount) {
        int sum = 0;
        for (int i = 0; i < 26; i++) {
            if (letterCount[i] > 0) {
                // 选择一个字母
                letterCount[i]--;
                // 递归调用深度优先搜索
                sum += 1 + dfs(letterCount);
                // 恢复状态，回溯
                letterCount[i]++;
            }
        }
        return sum;
    }
}
```


#### 104. Maximum Depth of Binary Tree
> 给定二叉树的根，返回其最大深度。
> 
> 二叉树的最大深度是从根节点向下到最远的叶节点的最长路径上的节点数。

```txt
Input: root = [3,9,20,null,null,15,7]
Output: 3
```

---

```java
class Solution {
    public int maxDepth(TreeNode root) {
        return dfs(root);
    }
    
    private int dfs(TreeNode node) {
        if (null == node)
            return 0;

        return Math.max(dfs(node.left), dfs(node.right)) + 1;
    }
}
```


#### 94. Binary Tree Inorder Traversal
> 给定二叉树的根，返回其节点值的中序遍历。

```txt
Input: root = [1,null,2,3]
Output: [1,3,2]
```

---

```java
class Solution {
    
    List<Integer> result;
    
    public List<Integer> inorderTraversal(TreeNode root) {
        result = new ArrayList<>();

        dfs(root);

        return result;    
    }

    private void dfs(TreeNode node) {
        if (node == null)
            return;
        
        dfs(node.left);
        result.add(node.val);
        dfs(node.right);
    }
}
```


#### 207. Course Schedule
> 您必须学习的课程总共有`numCourses`，标签从`0`到`numCourses-1`。
> 
> 您将获得一个数组 `prerequisites`，其中 `prerequisites[i]=[ai，bi]` 表示如果您想要学习课程 `ai`，您必须首先学习课程`bi`。
>
> 例如，对[0，1]表示要选修课程0，必须先选修课程1。
>
> 如果可以完成所有课程，则返回TRUE。否则，返回FALSE。

```txt
Example 1:

Input: numCourses = 2, prerequisites = [[1,0]]

Output: true

Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.
```

---

- graph: key-要学的课程，value-其全部前置课程
- 三种状态
  - 在这里，状态 1 表示正在访问的节点，有助于检测环的存在。当你在DFS过程中访问一个节点时，将其标记为1表示该节点正在当前的DFS遍历中被访问。如果在同一轮DFS中再次访问到了状态为1的节点，说明存在环。这就是为什么要有这个状态的原因。

```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        // 构建有向图
        List<List<Integer>> graph = new ArrayList<>();

        for (int i = 0; i < numCourses; i++) { 
            graph.add(new ArrayList<>()); // 必要，不然hasCycle中遍历可能会NPE
        }
        for (int[] prerequisite : prerequisites) {
            graph.get(prerequisite[0]).add(prerequisite[1]);
        }

        // 用数组来表示节点的状态，0表示未访问，1表示正在访问，2表示已完成访问
        int[] visited = new int[numCourses];

        // 对每个节点进行DFS
        for (int i = 0; i < numCourses; i++) {
            if (visited[i] == 0 && hasCycle(graph, visited, i)) {
                return false; // 存在环，不能完成所有课程
            }
        }

        return true; // 不存在环，可以完成所有课程
    }

    private boolean hasCycle(List<List<Integer>> graph, int[] visited, int course) {
        // 标记当前节点为正在访问
        visited[course] = 1;

        // 遍历当前节点的所有邻居
        for (int neighbor : graph.get(course)) {
            if (visited[neighbor] == 1) {
                return true; // 发现环
            }
         
            if (visited[neighbor] == 0 && hasCycle(graph, visited, neighbor)) {
                return true; // 递归遍历邻居节点
            }
        }

        // 标记当前节点为已完成访问
        visited[course] = 2;
        return false;
    }
}


```

##### 拓扑法
通过维护每门课程的入度（inDegree），在每一轮循环中移除入度为0的课程，直到所有课程都被移除或者无法再移除。
- 每门课程的入度表示有多少其他课程依赖于这门课程，即有多少先修课程。
- removed 数组标志已经移除的先修关系，
- totalRemoved 记录总共移除的先修关系数量
- currentRemoved 记录当前轮次移除的先修关系数量。

```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        int[] inDegree = new int[numCourses]; // 用来记录每门课程的入度
        for (int[] prerequisite : prerequisites) {
            inDegree[prerequisite[1]]++;
        }
        
        int totalRemoved = 0; // 记录已经移除的先修关系数量
        int[] removed = new int[prerequisites.length]; // 记录已经移除的先修关系的标志数组
        while (totalRemoved < prerequisites.length) {
            int currentRemoved = 0; // 记录当前轮次移除的先修关系数量
            for (int i = 0; i < prerequisites.length; i++) {
                if (removed[i] == 1) {
                    continue; // 如果该关系已经被移除，跳过
                }
                int[] prerequisite = prerequisites[i];
                if (inDegree[prerequisite[0]] == 0) {
                    // 如果当前先修课程入度为0，移除这个先修关系
                    inDegree[prerequisite[1]]--;
                    removed[i] = 1;
                    currentRemoved++;
                }
            }
            if (currentRemoved == 0) {
                return false; // 如果当前轮次没有移除任何先修关系，说明存在环
            }
            totalRemoved += currentRemoved; // 更新总的移除数量
        }
        return true;
    }
}

```
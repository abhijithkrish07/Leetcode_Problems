![image](https://github.com/user-attachments/assets/6f434e6a-9ce4-4176-8f58-6d5698c9c8b6)Medium - 14/10/2024

Q:
2530. Maximal Score After Applying K Operations

You are given a 0-indexed integer array nums and an integer k. You have a starting score of 0.

In one operation:

choose an index i such that 0 <= i < nums.length,
increase your score by nums[i], and
replace nums[i] with ceil(nums[i] / 3).
Return the maximum possible score you can attain after applying exactly k operations.

The ceiling function ceil(val) is the least integer greater than or equal to val.

 

Example 1:

Input: nums = [10,10,10,10,10], k = 5
Output: 50
Explanation: Apply the operation to each array element exactly once. The final score is 10 + 10 + 10 + 10 + 10 = 50.
Example 2:

Input: nums = [1,10,3,3,3], k = 3
Output: 17
Explanation: You can do the following operations:
Operation 1: Select i = 1, so nums becomes [1,4,3,3,3]. Your score increases by 10.
Operation 2: Select i = 1, so nums becomes [1,2,3,3,3]. Your score increases by 4.
Operation 3: Select i = 2, so nums becomes [1,1,1,3,3]. Your score increases by 3.
The final score is 10 + 4 + 3 = 17.

Code: 

```
import heapq
import math
class Solution:
    def maxKelements(self, nums: List[int], k: int) -> int:
        # Convert nums to a max-heap by pushing negative values
        # heap ensures when you pop, you always get the least value
        # when you make it negative, you always get the highest magnitude value
        max_heap = [-num for num in nums]
        heapq.heapify(max_heap)
        score = 0

        for _ in range(k):
        # Extract the maximum element (convert back to positive)
            max_element = -heapq.heappop(max_heap)
            score += max_element
            
            # Calculate the new value and push it back into the heap
            new_value = math.ceil(max_element / 3)
            heapq.heappush(max_heap, -new_value)

        return score
```
Medium - 15/10/2024

Q:
2938. Separate Black and White Balls

There are n balls on a table, each ball has a color black or white.

You are given a 0-indexed binary string s of length n, where 1 and 0 represent black and white balls, respectively.

In each step, you can choose two adjacent balls and swap them.

Return the minimum number of steps to group all the black balls to the right and all the white balls to the left.

 

Example 1:

Input: s = "101"
Output: 1
Explanation: We can group all the black balls to the right in the following way:
- Swap s[0] and s[1], s = "011".
Initially, 1s are not grouped together, requiring at least 1 step to group them to the right.
Example 2:

Input: s = "100"
Output: 2
Explanation: We can group all the black balls to the right in the following way:
- Swap s[0] and s[1], s = "010".
- Swap s[1] and s[2], s = "001".
It can be proven that the minimum number of steps needed is 2.
Example 3:

Input: s = "0111"
Output: 0
Explanation: All the black balls are already grouped to the right.

```
class Solution:
    def minimumSteps(self, s: str) -> int:
        steps = 0
        count_black = 0

        for ball in s:
            if(ball == '1'):
                count_black+=1
            else:
                steps+=count_black
        
        return steps
```

Code Explanation:
The black_count variable keeps track of the number of black balls ('1') encountered so far.
For each white ball ('0'), the number of steps required to move it past all the black balls encountered so far is added to steps.
This ensures that all white balls are moved to the left of all black balls with the minimum number of swaps.


1405. Longest Happy String

A string s is called happy if it satisfies the following conditions:

s only contains the letters 'a', 'b', and 'c'.
s does not contain any of "aaa", "bbb", or "ccc" as a substring.
s contains at most a occurrences of the letter 'a'.
s contains at most b occurrences of the letter 'b'.
s contains at most c occurrences of the letter 'c'.
Given three integers a, b, and c, return the longest possible happy string. If there are multiple longest happy strings, return any of them. If there is no such string, return the empty string "".

A substring is a contiguous sequence of characters within a string.

 

Example 1:

Input: a = 1, b = 1, c = 7
Output: "ccaccbcc"
Explanation: "ccbccacc" would also be a correct answer.
Example 2:

Input: a = 7, b = 1, c = 0
Output: "aabaa"
Explanation: It is the only correct answer in this case.

Code: 

```
import heapq

class Solution:
    def longestDiverseString(self, a: int, b: int, c: int) -> str:
        # Initialize a max-heap
        max_heap = []
        if a > 0:
            heapq.heappush(max_heap, (-a, 'a'))
        if b > 0:
            heapq.heappush(max_heap, (-b, 'b'))
        if c > 0:
            heapq.heappush(max_heap, (-c, 'c'))
        
        # Initialize result list
        result = []
        
        # Construct the string
        while max_heap:
            count1, char1 = heapq.heappop(max_heap)
            
            # Check if the last two characters are the same as the current character
            if len(result) >= 2 and result[-1] == result[-2] == char1:
                # If the heap is empty, break the loop
                if not max_heap:
                    break
                
                # Pop the next character from the heap
                count2, char2 = heapq.heappop(max_heap)
                result.append(char2)
                
                # If the next character still has remaining count, push it back onto the heap
                if count2 + 1 < 0:
                    heapq.heappush(max_heap, (count2 + 1, char2))
                
                # Push the current character back onto the heap
                heapq.heappush(max_heap, (count1, char1))
            else:
                # Append the current character to the result
                result.append(char1)
                
                # If the current character still has remaining count, push it back onto the heap
                if count1 + 1 < 0:
                    heapq.heappush(max_heap, (count1 + 1, char1))
        
        # Return the result as a string
        return ''.join(result)
```
670. Maximum Swap


You are given an integer num. You can swap two digits at most once to get the maximum valued number.
Return the maximum valued number you can get.

Example 1:

Input: num = 2736
Output: 7236
Explanation: Swap the number 2 and the number 7.
Example 2:

Input: num = 9973
Output: 9973
Explanation: No swap.

Code: Re-look
```
class Solution:
    def maximumSwap(self, num: int) -> int:
        # Step 1: Convert the integer to a string
        # Step 2: Convert the string to a list of characters (digits)
        digits = list(str(num))
        
        # Step 3: Implement a function to find the maximum number by swapping digits at most twice
        def swap_to_maximize(digits, swaps):
            n = len(digits)
            for i in range(n):
                if swaps == 0:
                    break
                # Find the maximum digit to the right of the current position
                max_digit = max(digits[i:])
                if digits[i] != max_digit:
                    # Find the rightmost occurrence of the max_digit
                    max_digit_index = ''.join(digits).rfind(max_digit)
                    print(max_digit_index)
                    # Swap the current digit with the max_digit
                    digits[i], digits[max_digit_index] = digits[max_digit_index], digits[i]
                    swaps -= 1
            return digits
        
        # Step 4: Use the function to maximize the number with at most 2 swaps
        max_digits = swap_to_maximize(digits, 1)
        
        # Convert the list of digits back to an integer
        max_num = int(''.join(max_digits))
        
        return max_num

```
2044. Count Number of Maximum Bitwise-OR Subsets - Need to relook

Given an integer array nums, find the maximum possible bitwise OR of a subset of nums and return the number of different non-empty subsets with the maximum bitwise OR.

An array a is a subset of an array b if a can be obtained from b by deleting some (possibly zero) elements of b. Two subsets are considered different if the indices of the elements chosen are different.

The bitwise OR of an array a is equal to a[0] OR a[1] OR ... OR a[a.length - 1] (0-indexed).


```
from itertools import combinations
class Solution:
    def countMaxOrSubsets(self, nums: List[int]) -> int:
        # Step 1: Calculate the maximum possible bitwise OR of the entire array
        max_or = 0
        for num in nums:
            max_or |= num
        
        # Step 2: Use a recursive function to count subsets with the maximum bitwise OR
        def dfs(index, current_or):
            nonlocal count
            if index == len(nums):
                if current_or == max_or:
                    count += 1
                return
            # Include the current element
            dfs(index + 1, current_or | nums[index])
            # Exclude the current element
            dfs(index + 1, current_or)
        
        count = 0
        dfs(0, 0)
        return count
```
1545. Find Kth Bit in Nth Binary String - Need to relook
Given two positive integers n and k, the binary string Sn is formed as follows:

S1 = "0"
Si = Si - 1 + "1" + reverse(invert(Si - 1)) for i > 1
Where + denotes the concatenation operation, reverse(x) returns the reversed string x, and invert(x) inverts all the bits in x (0 changes to 1 and 1 changes to 0).

For example, the first four strings in the above sequence are:

S1 = "0"
S2 = "011"
S3 = "0111001"
S4 = "011100110110001"
Return the kth bit in Sn. It is guaranteed that k is valid for the given n.
```
class Solution:
    def findKthBit(self, n: int, k: int) -> str:
        def find_kth_bit(n, k):
            if n == 1:
                return "0"
            length = (1 << n) - 1  # 2^n - 1
            mid = (length // 2) + 1
            if k == mid:
                return "1"
            elif k < mid:
                return find_kth_bit(n - 1, k)
            else:
                return '0' if find_kth_bit(n - 1, length - k + 1) == '1' else '1'
        
        return find_kth_bit(n, k)
```
1106. Parsing A Boolean Expression - Need to relook
Hard
A boolean expression is an expression that evaluates to either true or false. It can be in one of the following shapes:

't' that evaluates to true.
'f' that evaluates to false.
'!(subExpr)' that evaluates to the logical NOT of the inner expression subExpr.
'&(subExpr1, subExpr2, ..., subExprn)' that evaluates to the logical AND of the inner expressions subExpr1, subExpr2, ..., subExprn where n >= 1.
'|(subExpr1, subExpr2, ..., subExprn)' that evaluates to the logical OR of the inner expressions subExpr1, subExpr2, ..., subExprn where n >= 1.
Given a string expression that represents a boolean expression, return the evaluation of that expression.

It is guaranteed that the given expression is valid and follows the given rules.

```
class Solution:
    def parseBoolExpr(self, expression: str) -> bool:
        def parse_expression(expr: str) -> bool:
            if expr == 't':
                return True
            elif expr == 'f':
                return False
            elif expr.startswith('!'):
                return not parse_expression(expr[2:-1])
            elif expr.startswith('&'):
                sub_exprs = split_expressions(expr[2:-1])
                return all(parse_expression(sub) for sub in sub_exprs)
            elif expr.startswith('|'):
                sub_exprs = split_expressions(expr[2:-1])
                return any(parse_expression(sub) for sub in sub_exprs)
            else:
                raise ValueError("Invalid expression")

        def split_expressions(expr: str) -> list:
            sub_exprs = []
            balance = 0
            start = 0
            for i, char in enumerate(expr):
                if char == '(':
                    balance += 1
                elif char == ')':
                    balance -= 1
                elif char == ',' and balance == 0:
                    sub_exprs.append(expr[start:i])
                    start = i + 1
            sub_exprs.append(expr[start:])
            return sub_exprs

        return parse_expression(expression)
```

1593. Split a String Into the Max Number of Unique Substrings - Need to relook

Given a string s, return the maximum number of unique substrings that the given string can be split into.

You can split string s into any list of non-empty substrings, where the concatenation of the substrings forms the original string. However, you must split the substrings such that all of them are unique.

A substring is a contiguous sequence of characters within a string.

 

Example 1:

Input: s = "ababccc"
Output: 5
Explanation: One way to split maximally is ['a', 'b', 'ab', 'c', 'cc']. Splitting like ['a', 'b', 'a', 'b', 'c', 'cc'] is not valid as you have 'a' and 'b' multiple times.


Code:

```
class Solution:
    def maxUniqueSplit(self, s: str) -> int:
        def backtrack(start: int, seen: set) -> int:
            if start == len(s):
                return len(seen)
            
            max_count = 0
            for end in range(start + 1, len(s) + 1):
                substring = s[start:end]
                if substring not in seen:
                    seen.add(substring)
                    max_count = max(max_count, backtrack(end, seen))
                    seen.remove(substring)
            
            return max_count
        
        return backtrack(0, set())
```
2583. Kth Largest Sum in a Binary Tree - need to relook

You are given the root of a binary tree and a positive integer k.

The level sum in the tree is the sum of the values of the nodes that are on the same level.

Return the kth largest level sum in the tree (not necessarily distinct). If there are fewer than k levels in the tree, return -1.

Note that two nodes are on the same level if they have the same distance from the root.

Example 1:


Input: root = [5,8,9,2,1,3,7,4,6], k = 2

![image](https://github.com/user-attachments/assets/4e8b2ec5-da53-4a68-845e-a550b6892db4)

Output: 13

Explanation: The level sums are the following:
- Level 1: 5.
- Level 2: 8 + 9 = 17.
- Level 3: 2 + 1 + 3 + 7 = 13.
- Level 4: 4 + 6 = 10.
The 2nd largest level sum is 13.

CODE:
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def kthLargestLevelSum(self, root: Optional[TreeNode], k: int) -> int:
        if not root:
            return -1

        # Perform level order traversal to calculate level sums
        level_sums = []
        queue = deque([root])
        
        while queue:
            level_size = len(queue)
            level_sum = 0
            
            for _ in range(level_size):
                node = queue.popleft()
                level_sum += node.val
                
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
            
            level_sums.append(level_sum)
        
        # Sort the level sums in descending order
        level_sums.sort(reverse=True)
        
        # Return the kth largest level sum if it exists
        if k <= len(level_sums):
            return level_sums[k - 1]
        else:
            return -1
```
2641. Cousins in Binary Tree II

Given the root of a binary tree, replace the value of each node in the tree with the sum of all its cousins' values.

Two nodes of a binary tree are cousins if they have the same depth with different parents.

Return the root of the modified tree.

Note that the depth of a node is the number of edges in the path from the root node to it.

Example 1:


Input: root = [5,4,9,1,10,null,7]
Output: [0,0,0,7,7,null,11]
![image](https://github.com/user-attachments/assets/069d478f-d518-45b8-811c-06b71d8d27e8)

Explanation: The diagram above shows the initial binary tree and the binary tree after changing the value of each node.
- Node with value 5 does not have any cousins so its sum is 0.
- Node with value 4 does not have any cousins so its sum is 0.
- Node with value 9 does not have any cousins so its sum is 0.
- Node with value 1 has a cousin with value 7 so its sum is 7.
- Node with value 10 has a cousin with value 7 so its sum is 7.
- Node with value 7 has cousins with values 1 and 10 so its sum is 11.

```
import java.util.*;

class Solution {

    public TreeNode replaceValueInTree(TreeNode root) {
        if (root == null) return root;

        Queue<TreeNode> nodeQueue = new LinkedList<>();
        nodeQueue.offer(root);
        List<Integer> levelSums = new ArrayList<>();

        // First BFS: Calculate sum of nodes at each level
        while (!nodeQueue.isEmpty()) {
            int levelSum = 0;
            int levelSize = nodeQueue.size();
            for (int i = 0; i < levelSize; ++i) {
                TreeNode currentNode = nodeQueue.poll();
                levelSum += currentNode.val;
                if (currentNode.left != null) nodeQueue.offer(currentNode.left);
                if (currentNode.right != null) nodeQueue.offer(currentNode.right);
            }
            levelSums.add(levelSum);
        }

        // Second BFS: Update each node's value to sum of its cousins
        nodeQueue.offer(root);
        int levelIndex = 1;
        root.val = 0; // Root has no cousins
        while (!nodeQueue.isEmpty()) {
            int levelSize = nodeQueue.size();
            for (int i = 0; i < levelSize; ++i) {
                TreeNode currentNode = nodeQueue.poll();
                int siblingSum = (currentNode.left != null ? currentNode.left.val : 0) + (currentNode.right != null ? currentNode.right.val : 0);
                
                if (currentNode.left != null) {
                    currentNode.left.val = levelSums.get(levelIndex) - siblingSum;
                    nodeQueue.offer(currentNode.left);
                }
                if (currentNode.right != null) {
                    currentNode.right.val = levelSums.get(levelIndex) - siblingSum;
                    nodeQueue.offer(currentNode.right);
                }
            }
            ++levelIndex;
        }

        return root;
    }
}
```

951. Flip Equivalent Binary Trees - Need to relook

For a binary tree T, we can define a flip operation as follows: choose any node, and swap the left and right child subtrees.

A binary tree X is flip equivalent to a binary tree Y if and only if we can make X equal to Y after some number of flip operations.

Given the roots of two binary trees root1 and root2, return true if the two trees are flip equivalent or false otherwise.

Example 1 <br>

![image](https://github.com/user-attachments/assets/b46e450d-98ea-4b88-83a9-43486c14005e)

Input: root1 = [1,2,3,4,5,6,null,null,null,7,8], root2 = [1,3,2,null,6,4,5,null,null,null,null,8,7]
Output: true
Explanation: We flipped at nodes with values 1, 3, and 5.

Example 2:

Input: root1 = [], root2 = []
Output: true
Example 3:

Input: root1 = [], root2 = [1]
Output: false

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public boolean flipEquiv(TreeNode root1, TreeNode root2) {
 // Base cases
        if (root1 == null && root2 == null) return true;
        if (root1 == null || root2 == null) return false;
        if (root1.val != root2.val) return false;

        // Check if children are flip equivalent in either original or flipped state
        boolean flipEquiv = (flipEquiv(root1.left, root2.left) && flipEquiv(root1.right, root2.right)) ||
                            (flipEquiv(root1.left, root2.right) && flipEquiv(root1.right, root2.left));

        return flipEquiv;
    }
}
```

1233. Remove Sub-Folders from the Filesystem

Given a list of folders folder, return the folders after removing all sub-folders in those folders. You may return the answer in any order.

If a folder[i] is located within another folder[j], it is called a sub-folder of it. A sub-folder of folder[j] must start with folder[j], followed by a "/". For example, "/a/b" is a sub-folder of "/a", but "/b" is not a sub-folder of "/a/b/c".

The format of a path is one or more concatenated strings of the form: '/' followed by one or more lowercase English letters.

For example, "/leetcode" and "/leetcode/problems" are valid paths while an empty string and "/" are not.
 

Example 1:

Input: folder = ["/a","/a/b","/c/d","/c/d/e","/c/f"]
Output: ["/a","/c/d","/c/f"]
Explanation: Folders "/a/b" is a subfolder of "/a" and "/c/d/e" is inside of folder "/c/d" in our filesystem.

```
class Solution:
    def removeSubfolders(self, folder: List[str]) -> List[str]:
        # Step 1: Sort the folders lexicographically
        folder.sort()
        
        # Step 2: Initialize the result list and the previous folder variable
        result = []
        prev = ""
        
        # Step 3: Iterate through each folder
        for f in folder:
            # Step 4: Check if the current folder is a sub-folder of the previous folder
            if not prev or not f.startswith(prev + "/"):
                result.append(f)
                prev = f
        
        # Step 5: Return the result list
        return result
```
2458. Height of Binary Tree After Subtree Removal Queries

You are given the root of a binary tree with n nodes. Each node is assigned a unique value from 1 to n. You are also given an array queries of size m.

You have to perform m independent queries on the tree where in the ith query you do the following:

Remove the subtree rooted at the node with the value queries[i] from the tree. It is guaranteed that queries[i] will not be equal to the value of the root.
Return an array answer of size m where answer[i] is the height of the tree after performing the ith query.

Note:

The queries are independent, so the tree returns to its initial state after each query.
The height of a tree is the number of edges in the longest simple path from the root to some node in the tree.

![image](https://github.com/user-attachments/assets/6afd7866-3924-4a20-a3d6-15911472b8d1)

Input: root = [1,3,4,2,null,6,5,null,null,null,null,null,7], queries = [4]
Output: [2]
Explanation: The diagram above shows the tree after removing the subtree rooted at node with value 4.
The height of the tree is 2 (The path 1 -> 3 -> 2).

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {

    // Map to store the height of each node
    private Map<Integer, Integer> heights = new HashMap<>();
    // Map to store the maximum height of the tree after removing each node
    private Map<Integer, Integer> removalHeights = new HashMap<>();
    private int currentMaxHeight = 0;

    public int[] treeQueries(TreeNode root, int[] queries) {
        computeHeights(root);
        currentMaxHeight = 0; // Reset for the second traversal
        traverseLeftToRight(root, 0);
        currentMaxHeight = 0; // Reset for the second traversal
        traverseRightToLeft(root, 0);

        // Process queries and build the result array
        int queryCount = queries.length;
        int[] queryResults = new int[queryCount];
        for (int i = 0; i < queryCount; i++) {
            queryResults[i] = removalHeights.get(queries[i]);
        }

        return queryResults;
    }

    private int computeHeights(TreeNode node) {
        if (node == null) {
            return -1;
        }
        int leftHeight = computeHeights(node.left);
        int rightHeight = computeHeights(node.right);
        int height = 1 + Math.max(leftHeight, rightHeight);
        heights.put(node.val, height);
        return height;
    }

    private void traverseLeftToRight(TreeNode node, int currentHeight) {
        if (node == null) return;

        // Store the maximum height if this node were removed
        removalHeights.put(node.val, currentMaxHeight);

        // Update the current maximum height
        currentMaxHeight = Math.max(currentMaxHeight, currentHeight);

        // Traverse left subtree first, then right
        traverseLeftToRight(node.left, currentHeight + 1);
        traverseLeftToRight(node.right, currentHeight + 1);
    }

    private void traverseRightToLeft(TreeNode node, int currentHeight) {
        if (node == null) return;

        // Update the maximum height if this node were removed
        removalHeights.put(node.val, Math.max(removalHeights.get(node.val), currentMaxHeight));

        // Update the current maximum height
        currentMaxHeight = Math.max(currentHeight, currentMaxHeight);

        // Traverse right subtree first, then left
        traverseRightToLeft(node.right, currentHeight + 1);
        traverseRightToLeft(node.left, currentHeight + 1);
    }
}
```

Editoral Soln:
```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {

    // Array to store the maximum height of the tree after removing each node
    static final int[] maxHeightAfterRemoval = new int[100001];

    int currentMaxHeight = 0;

    public int[] treeQueries(TreeNode root, int[] queries) {
        traverseLeftToRight(root, 0);
        currentMaxHeight = 0; // Reset for the second traversal
        traverseRightToLeft(root, 0);

        // Process queries and build the result array
        int queryCount = queries.length;
        int[] queryResults = new int[queryCount];
        for (int i = 0; i < queryCount; i++) {
            queryResults[i] = maxHeightAfterRemoval[queries[i]];
        }

        return queryResults;
    }

    private void traverseLeftToRight(TreeNode node, int currentHeight) {
        if (node == null) return;

        // Store the maximum height if this node were removed
        maxHeightAfterRemoval[node.val] = currentMaxHeight;

        // Update the current maximum height
        currentMaxHeight = Math.max(currentMaxHeight, currentHeight);

        // Traverse left subtree first, then right
        traverseLeftToRight(node.left, currentHeight + 1);
        traverseLeftToRight(node.right, currentHeight + 1);
    }

    private void traverseRightToLeft(TreeNode node, int currentHeight) {
        if (node == null) return;

        // Update the maximum height if this node were removed
        maxHeightAfterRemoval[node.val] = Math.max(
            maxHeightAfterRemoval[node.val],
            currentMaxHeight
        );

        // Update the current maximum height
        currentMaxHeight = Math.max(currentHeight, currentMaxHeight);

        // Traverse right subtree first, then left
        traverseRightToLeft(node.right, currentHeight + 1);
        traverseRightToLeft(node.left, currentHeight + 1);
    }
}
```
https://leetcode.com/problems/longest-square-streak-in-an-array/

```
import java.util.Arrays;
import java.util.HashSet;
import java.util.Set;

class Solution {

    public int longestSquareStreak(int[] nums) {
        Arrays.sort(nums);
        Set<Integer> processedNumbers = new HashSet<>();
        int longestStreak = -1;

        for (int current : nums) {
            if (processedNumbers.contains(current)) continue;

            int streak = current;
            int streakLength = 1;

            while (true) {
                if ((long) streak * (long) streak > 1e5) break;
                if (binarySearch(nums, streak * streak)) {
                    streak *= streak;
                    processedNumbers.add(streak);
                    streakLength++;
                } else {
                    break;
                }
            }

            if (streakLength > 1 && streakLength > longestStreak) {
                longestStreak = streakLength;
            }
        }

        return longestStreak < 2 ? -1 : longestStreak;
    }

    private boolean binarySearch(int[] nums, int target) {
        if (target < 0) return false;

        int left = 0;
        int right = nums.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) return true;
            if (nums[mid] > target) right = mid - 1;
            else left = mid + 1;
        }

        return false;
    }
}
```

2684. Maximum Number of Moves in a Grid

You are given a 0-indexed m x n matrix grid consisting of positive integers.

You can start at any cell in the first column of the matrix, and traverse the grid in the following way:

From a cell (row, col), you can move to any of the cells: (row - 1, col + 1), (row, col + 1) and (row + 1, col + 1) such that the value of the cell you move to, should be strictly bigger than the value of the current cell.
Return the maximum number of moves that you can perform.

Example 1:
![image](https://github.com/user-attachments/assets/9678742f-44e2-43d4-af57-a27737f371c4)
<br>

Input: grid = [[2,4,3,5],[5,4,9,3],[3,4,2,11],[10,9,13,15]]
Output: 3
Explanation: We can start at the cell (0, 0) and make the following moves:
- (0, 0) -> (0, 1).
- (0, 1) -> (1, 2).
- (1, 2) -> (2, 3).
It can be shown that it is the maximum number of moves that can be made.

```
public class Solution {
    private int[][] memo;
    private int[][] grid;
    private int m, n;

    public int maxMoves(int[][] grid) {
        this.grid = grid;
        this.m = grid.length;
        this.n = grid[0].length;
        this.memo = new int[m][n];

        int maxResult = 0;
        for (int row = 0; row < m; row++) {
            maxResult = Math.max(maxResult, dfs(row, 0));
        }
        return maxResult;
    }

    private int dfs(int row, int col) {
        if (memo[row][col] != 0) {
            return memo[row][col];
        }

        int maxMoves = 0;
        int[][] directions = {{-1, 1}, {0, 1}, {1, 1}};
        for (int[] dir : directions) {
            int newRow = row + dir[0];
            int newCol = col + dir[1];
            if (newRow >= 0 && newRow < m && newCol < n && grid[newRow][newCol] > grid[row][col]) {
                maxMoves = Math.max(maxMoves, 1 + dfs(newRow, newCol));
            }
        }

        memo[row][col] = maxMoves;
        return maxMoves;
    }
}
```
1671. Minimum Number of Removals to Make Mountain Array

You may recall that an array arr is a mountain array if and only if:

arr.length >= 3
There exists some index i (0-indexed) with 0 < i < arr.length - 1 such that:
arr[0] < arr[1] < ... < arr[i - 1] < arr[i]
arr[i] > arr[i + 1] > ... > arr[arr.length - 1]
Given an integer array nums​​​, return the minimum number of elements to remove to make nums​​​ a mountain array.

```
from typing import List
import bisect

class Solution:
    def minimumMountainRemovals(self, nums: List[int]) -> int:
        n = len(nums)
        if n < 3:
            return 0

        # Function to calculate LIS ending at each index
        def calculate_lis(nums):
            lis = [0] * n
            seq = []
            for i in range(n):
                pos = bisect.bisect_left(seq, nums[i])
                if pos == len(seq):
                    seq.append(nums[i])
                else:
                    seq[pos] = nums[i]
                lis[i] = pos + 1
            return lis

        # Calculate LIS from left to right
        inc = calculate_lis(nums)

        # Calculate LIS from right to left (LDS)
        dec = calculate_lis(nums[::-1])[::-1]

        # Find the maximum value of inc[i] + dec[i] - 1
        max_len = 0
        for i in range(1, n-1):
            if inc[i] > 1 and dec[i] > 1:
                max_len = max(max_len, inc[i] + dec[i] - 1)

        # Calculate the minimum number of removals
        return n - max_len

```
Delete Characters to Make Fancy String

A fancy string is a string where no three consecutive characters are equal.

Given a string s, delete the minimum possible number of characters from s to make it fancy.

Return the final string after the deletion. It can be shown that the answer will always be unique.

 

Example 1:

Input: s = "leeetcode"
Output: "leetcode"
Explanation:
Remove an 'e' from the first group of 'e's to create "leetcode".
No three consecutive characters are equal, so return "leetcode".

```
class Solution {
    public String makeFancyString(String s) {
        StringBuilder result = new StringBuilder();
        char prev = s.charAt(0);
        int count = 1;
        result.append(prev);

        for (int i = 1; i < s.length(); i++) {
            if (s.charAt(i) == prev) {
                count++;
            } else {
                prev = s.charAt(i);
                count = 1;
            }

            if (count < 3) {
                result.append(s.charAt(i));
            }
        }

        return result.toString();
    }
}
```
2490. Circular Sentence

A sentence is a list of words that are separated by a single space with no leading or trailing spaces.

For example, "Hello World", "HELLO", "hello world hello world" are all sentences.
Words consist of only uppercase and lowercase English letters. Uppercase and lowercase English letters are considered different.

A sentence is circular if:

The last character of a word is equal to the first character of the next word.
The last character of the last word is equal to the first character of the first word.
For example, "leetcode exercises sound delightful", "eetcode", "leetcode eats soul" are all circular sentences. However, "Leetcode is cool", "happy Leetcode", "Leetcode" and "I like Leetcode" are not circular sentences.

Given a string sentence, return true if it is circular. Otherwise, return false.

Example 1:

Input: sentence = "leetcode exercises sound delightful"
Output: true
Explanation: The words in sentence are ["leetcode", "exercises", "sound", "delightful"].
- leetcode's last character is equal to exercises's first character.
- exercises's last character is equal to sound's first character.
- sound's last character is equal to delightful's first character.
- delightful's last character is equal to leetcode's first character.
The sentence is circular.
Example 2:

Input: sentence = "eetcode"
Output: true
Explanation: The words in sentence are ["eetcode"].
- eetcode's last character is equal to eetcode's first character.
The sentence is circular.

```
class Solution {
    public boolean isCircularSentence(String s) {
        int n = s.length();
        if(s.charAt(0) != s.charAt(n-1)){
            return false;
        }

        for(int i = 0;i<n;i++){
            if(s.charAt(i) == ' ' && s.charAt(i-1) != s.charAt(i+1)){
                return false;
            }
        }

        return true;   
    }
}
```
796. Rotate String
Given two strings s and goal, return true if and only if s can become goal after some number of shifts on s.

A shift on s consists of moving the leftmost character of s to the rightmost position.

For example, if s = "abcde", then it will be "bcdea" after one shift.
 

Example 1:

Input: s = "abcde", goal = "cdeab"
Output: true
Example 2:

Input: s = "abcde", goal = "abced"
Output: false

Code:
```
class Solution {
    public boolean rotateString(String s, String goal) {
        if (s.length() != goal.length()) {
            return false;
        }
        return (s + s).contains(goal);
    }
}
```
3163. String Compression III

Given a string word, compress it using the following algorithm:

Begin with an empty string comp. While word is not empty, use the following operation:
Remove a maximum length prefix of word made of a single character c repeating at most 9 times.
Append the length of the prefix followed by c to comp.
Return the string comp.

```
class Solution {
    public String compressedString(String word) {
        if (word == null || word.isEmpty()) {
            return "";
        }

        StringBuilder res = new StringBuilder();
        char prev = word.charAt(0);
        int count = 1;

        for (int i = 1; i < word.length(); i++) {
            char letter = word.charAt(i);
            if (prev == letter) {
                count++;
                if (count == 10) {
                    res.append(count - 1).append(prev);
                    count = 1;
                }
            } else {
                res.append(count).append(prev);
                prev = letter;
                count = 1;
            }
        }
        res.append(count).append(prev);

        return res.toString();
    }
}
```
```
class Solution:
    def compressedString(self, word: str) -> str:
        prev = word[0]
        result = ""
        count = 1
        for i in range (1,len(word)):
            if word[i] == prev:
                if count + 1 > 9:
                    result = result + str(count) + prev
                    count = 1
                else:
                    count+=1
            else:
                result = result + str(count) + prev
                count = 1
                prev = word[i]
            
        
        return result + str(count) + prev

```

2914. Minimum Number of Changes to Make Binary String Beautiful

You are given a 0-indexed binary string s having an even length.

A string is beautiful if it's possible to partition it into one or more substrings such that:

Each substring has an even length.
Each substring contains only 1's or only 0's.
You can change any character in s to 0 or 1.

Return the minimum number of changes required to make the string s beautiful.

 

Example 1:

Input: s = "1001"
Output: 2
Explanation: We change s[1] to 1 and s[3] to 0 to get string "1100".
It can be seen that the string "1100" is beautiful because we can partition it into "11|00".
It can be proven that 2 is the minimum number of changes needed to make the string beautiful.
Example 2:

Input: s = "10"
Output: 1
Explanation: We change s[1] to 1 to get string "11".
It can be seen that the string "11" is beautiful because we can partition it into "11".
It can be proven that 1 is the minimum number of changes needed to make the string beautiful.
Example 3:

Input: s = "0000"
Output: 0
Explanation: We don't need to make any changes as the string "0000" is beautiful already.
 

Constraints:

2 <= s.length <= 105
s has an even length.
s[i] is either '0' or '1'.
```
class Solution {
    public int minChanges(String s) {
        int changes = 0;
        for( int i =0; i<s.length();i+=2){
            if(s.charAt(i) != s.charAt(i+1)){
                ++changes;
            }
        }
        return changes;   
    }
}
```
```
class Solution:
    def minChanges(self, s: str) -> int:
        changes = 0
        for i in range(0, len(s), 2):
            if s[i] != s[i + 1]:
                changes += 1
        return changes

```

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
x
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
3011. Find if Array Can Be Sorted

You are given a 0-indexed array of positive integers nums.

In one operation, you can swap any two adjacent elements if they have the same number of 
set bits
. You are allowed to do this operation any number of times (including zero).

Return true if you can sort the array, else return false.

 

Example 1:

Input: nums = [8,4,2,30,15]
Output: true
Explanation: Let's look at the binary representation of every element. The numbers 2, 4, and 8 have one set bit each with binary representation "10", "100", and "1000" respectively. The numbers 15 and 30 have four set bits each with binary representation "1111" and "11110".
We can sort the array using 4 operations:
- Swap nums[0] with nums[1]. This operation is valid because 8 and 4 have one set bit each. The array becomes [4,8,2,30,15].
- Swap nums[1] with nums[2]. This operation is valid because 8 and 2 have one set bit each. The array becomes [4,2,8,30,15].
- Swap nums[0] with nums[1]. This operation is valid because 4 and 2 have one set bit each. The array becomes [2,4,8,30,15].
- Swap nums[3] with nums[4]. This operation is valid because 30 and 15 have four set bits each. The array becomes [2,4,8,15,30].
The array has become sorted, hence we return true.
Note that there may be other sequences of operations which also sort the array.

```
class Solution {
    public boolean canSortArray(int[] nums) {
        int n = nums.length;
        int ones[] = new int[n];
        Arrays.fill(ones,0);
        for(int i = 0 ; i< n; i++){
            String binary = Integer.toBinaryString(nums[i]);
            for(int j = 0 ; j< binary.length(); j++){
                if(binary.charAt(j) == '1'){
                    ++ones[i];
                }
            }
        }
        

        for(int i = 1 ; i< n; i++){
            int j = i - 1;
            while(j >= 0 && nums[j] > nums[j+1] && ones[j] == ones[j+1]){
                int temp = nums[j];
                nums[j] = nums[j+1];
                nums[j+1] = temp;
                --j;
            }
        }

        for(int i = 0 ; i< n - 1; i++){
            if(nums[i] > nums[i+1]){
                return false;
            }
        }

        return true;
    }
}

```
2275. Largest Combination With Bitwise AND Greater Than Zero
The bitwise AND of an array nums is the bitwise AND of all integers in nums.

For example, for nums = [1, 5, 3], the bitwise AND is equal to 1 & 5 & 3 = 1.
Also, for nums = [7], the bitwise AND is 7.
You are given an array of positive integers candidates. Evaluate the bitwise AND of every combination of numbers of candidates. Each number in candidates may only be used once in each combination.

Return the size of the largest combination of candidates with a bitwise AND greater than 0.

 

Example 1:

Input: candidates = [16,17,71,62,12,24,14]
Output: 4
Explanation: The combination [16,17,62,24] has a bitwise AND of 16 & 17 & 62 & 24 = 16 > 0.
The size of the combination is 4.
It can be shown that no combination with a size greater than 4 has a bitwise AND greater than 0.
Note that more than one combination may have the largest size.
For example, the combination [62,12,24,14] has a bitwise AND of 62 & 12 & 24 & 14 = 8 > 0.

```
import java.util.*;

class Solution {
    public int largestCombination(int[] candidates) {
        int[] bitCounts = new int[32];

        // Count the number of set bits at each bit position
        for (int num : candidates) {
            for (int bit = 0; bit < 32; bit++) {
                // System.out.println(num + " bit " + bit + " c "+ ((num & (1 << bit)));
                if ((num & (1 << bit)) != 0) {
                    bitCounts[bit]++;
                }
            }
        }

        // Find the maximum count of set bits at any position
        int maxCombinationSize = 0;
        for (int count : bitCounts) {
            maxCombinationSize = Math.max(maxCombinationSize, count);
        }

        return maxCombinationSize;
    }
}
```
3133. Minimum Array End

You are given two integers n and x. You have to construct an array of positive integers nums of size n where for every 0 <= i < n - 1, nums[i + 1] is greater than nums[i], and the result of the bitwise AND operation between all elements of nums is x.

Return the minimum possible value of nums[n - 1].

 

Example 1:

Input: n = 3, x = 4

Output: 6

Explanation:

nums can be [4,5,6] and its last element is 6.

Example 2:

Input: n = 2, x = 7

Output: 15

Explanation:

nums can be [7,15] and its last element is 15.
```
class Solution {

    public long minEnd(int n, int x) {
        long op = x;
        while (--n > 0) {
            op = (op + 1) | x;
        }

        return op;
    }
}
```
3097. Shortest Subarray With OR at Least K II

You are given an array nums of non-negative integers and an integer k.

An array is called special if the bitwise OR of all of its elements is at least k.

Return the length of the shortest special non-empty 
subarray
 of nums, or return -1 if no special subarray exists.

 

Example 1:

Input: nums = [1,2,3], k = 2

Output: 1

Explanation:

The subarray [3] has OR value of 3. Hence, we return 1.
```
class Solution {

    public int minimumSubarrayLength(int[] nums, int k) {
        int left = 1;
        int right = nums.length;
        int minLength = -1;

        // Binary search on the length of subarray
        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (hasValidSubarray(nums, k, mid)) {
                minLength = mid;
                right = mid - 1; // Try to find smaller length
            } else {
                left = mid + 1; // Try larger length
            }
        }

        return minLength;
    }

    private boolean hasValidSubarray(int[] nums, int k, int length) {
        int n = nums.length;
        for (int i = 0; i <= n - length; i++) {
            int current_or = 0;
            for (int j = i; j < i + length; j++) {
                current_or |= nums[j];
            }
            if (current_or >= k) {
                return true;
            }
        }
        return false;
    }
}
```
2601. Prime Subtraction Operation

You are given a 0-indexed integer array nums of length n.

You can perform the following operation as many times as you want:

Pick an index i that you haven’t picked before, and pick a prime p strictly less than nums[i], then subtract p from nums[i].
Return true if you can make nums a strictly increasing array using the above operation and false otherwise.

A strictly increasing array is an array whose each element is strictly greater than its preceding element.

 

Example 1:

Input: nums = [4,9,6,10]
Output: true
Explanation: In the first operation: Pick i = 0 and p = 3, and then subtract 3 from nums[0], so that nums becomes [1,9,6,10].
In the second operation: i = 1, p = 7, subtract 7 from nums[1], so nums becomes equal to [1,2,6,10].
After the second operation, nums is sorted in strictly increasing order, so the answer is true.

```
import java.util.ArrayList;
import java.util.List;

public class Solution {

    // Helper function to check if a number is prime
    public static boolean isPrime(int n) {
        if (n <= 1) return false;
        for (int i = 2; i * i <= n; i++) {
            if (n % i == 0) return false;
        }
        return true;
    }

    // Helper function to get all prime numbers less than a given number
    public static List<Integer> getPrimesLessThan(int n) {
        List<Integer> primes = new ArrayList<>();
        for (int i = 2; i < n; i++) {
            if (isPrime(i)) {
                primes.add(i);
            }
        }
        return primes;
    }

    // Function to check if the array can be made strictly increasing
    public static boolean primeSubOperation(int[] nums) {
        int n = nums.length;
        boolean[] used = new boolean[n];
        
        for (int i = 0; i < n; i++) {
            List<Integer> primes = getPrimesLessThan(nums[i]);
            for (int j = primes.size() - 1; j >= 0; j--) {
                int p = primes.get(j);
                if (nums[i] - p > (i > 0 ? nums[i - 1] : Integer.MIN_VALUE)) {
                    nums[i] -= p;
                    used[i] = true;
                    break;
                }
            }
        }

        for (int i = 1; i < n; i++) {
            if (nums[i] <= nums[i - 1]) {
                return false;
            }
        }
        return true;
    }
}
```
2070. Most Beautiful Item for Each Query
You are given a 2D integer array items where items[i] = [pricei, beautyi] denotes the price and beauty of an item respectively.

You are also given a 0-indexed integer array queries. For each queries[j], you want to determine the maximum beauty of an item whose price is less than or equal to queries[j]. If no such item exists, then the answer to this query is 0.

Return an array answer of the same length as queries where answer[j] is the answer to the jth query.

 

Example 1:

Input: items = [[1,2],[3,2],[2,4],[5,6],[3,5]], queries = [1,2,3,4,5,6]
Output: [2,4,5,5,6,6]
Explanation:
- For queries[0]=1, [1,2] is the only item which has price <= 1. Hence, the answer for this query is 2.
- For queries[1]=2, the items which can be considered are [1,2] and [2,4]. 
  The maximum beauty among them is 4.
- For queries[2]=3 and queries[3]=4, the items which can be considered are [1,2], [3,2], [2,4], and [3,5].
  The maximum beauty among them is 5.
- For queries[4]=5 and queries[5]=6, all items can be considered.
  Hence, the answer for them is the maximum beauty of all items, i.e., 6.

```
from bisect import bisect_right

class Solution:
    def maximumBeauty(self, items, queries):
        # Sort items by price
        items.sort()
        
        # Precompute the maximum beauty for each price
        max_beauties = []
        current_max = 0
        for price, beauty in items:
            current_max = max(current_max, beauty)
            max_beauties.append((price, current_max))
        
        # Function to find the maximum beauty for a given query
        def find_max_beauty(query):
            idx = bisect_right(max_beauties, (query, float('inf'))) - 1
            return max_beauties[idx][1] if idx >= 0 else 0
        
        # Compute the result for each query
        return [find_max_beauty(query) for query in queries]
```
2563. Count the Number of Fair Pairs

Given a 0-indexed integer array nums of size n and two integers lower and upper, return the number of fair pairs.

A pair (i, j) is fair if:

0 <= i < j < n, and
lower <= nums[i] + nums[j] <= upper
 

Example 1:

Input: nums = [0,1,7,4,4,5], lower = 3, upper = 6
Output: 6
Explanation: There are 6 fair pairs: (0,3), (0,4), (0,5), (1,3), (1,4), and (1,5).

```
import java.util.Arrays;

class Solution {
    public long countFairPairs(int[] nums, int lower, int upper) {
        Arrays.sort(nums);
        int n = nums.length;
        long count = 0;

        for (int i = 0; i < n; i++) {
            int left = i + 1;
            int right = n - 1;

            while (left <= right) {
                int mid = left + (right - left) / 2;
                if (nums[i] + nums[mid] < lower) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }
            int low = left;

            left = i + 1;
            right = n - 1;

            while (left <= right) {
                int mid = left + (right - left) / 2;
                if (nums[i] + nums[mid] <= upper) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }
            int high = right;

            count += (high - low + 1);
        }

        return count;
    }
}
```
862. Shortest Subarray with Sum at Least K

Given an integer array nums and an integer k, return the length of the shortest non-empty subarray of nums with a sum of at least k. If there is no such subarray, return -1.

A subarray is a contiguous part of an array.

 

Example 1:

Input: nums = [1], k = 1
Output: 1
Example 2:

Input: nums = [1,2], k = 4
Output: -1
Example 3:

Input: nums = [2,-1,2], k = 3
Output: 3

```
import java.util.Deque;
import java.util.LinkedList;

class Solution {
    public int shortestSubarray(int[] nums, int k) {
        int n = nums.length;
        Deque<Integer> deque = new LinkedList<>();
        long[] prefixSum = new long[n + 1];
        for (int i = 0; i < n; i++) {
            prefixSum[i + 1] = prefixSum[i] + nums[i];
        }
        int minLength = Integer.MAX_VALUE;
        for (int i = 0; i <= n; i++) {
            while (!deque.isEmpty() && prefixSum[i] - prefixSum[deque.peekFirst()] >= k) {
                minLength = Math.min(minLength, i - deque.pollFirst());
            }
            while (!deque.isEmpty() && prefixSum[i] <= prefixSum[deque.peekLast()]) {
                deque.pollLast();
            }
            deque.addLast(i);
        }
        return minLength == Integer.MAX_VALUE ? -1 : minLength;
    }
}
```

1652. Defuse the Bomb

You have a bomb to defuse, and your time is running out! Your informer will provide you with a circular array code of length of n and a key k.

To decrypt the code, you must replace every number. All the numbers are replaced simultaneously.

If k > 0, replace the ith number with the sum of the next k numbers.
If k < 0, replace the ith number with the sum of the previous k numbers.
If k == 0, replace the ith number with 0.
As code is circular, the next element of code[n-1] is code[0], and the previous element of code[0] is code[n-1].

Given the circular array code and an integer key k, return the decrypted code to defuse the bomb!

 

Example 1:

Input: code = [5,7,1,4], k = 3
Output: [12,10,16,13]
Explanation: Each number is replaced by the sum of the next 3 numbers. The decrypted code is [7+1+4, 1+4+5, 4+5+7, 5+7+1]. Notice that the numbers wrap around.

```
class Solution {
    public int[] decrypt(int[] nums, int k) {
        int n = nums.length;
        int[] sum = new int[n];
        Arrays.fill(sum,0);
        if(k>0){
            for(int i = 0;i<n;i++){
                int counter = 0;
                int x = i;
                while(counter<k){
                    ++x;
                    sum[i] += nums[x%n];
                    ++counter;  
                }
            }
        } else if(k<0){
            for(int i = 0;i<n;i++){
                int x = n - 1 + i;
                int counter = k; 
                while(counter<0){
                    sum[i] += nums[x%n];
                    ++counter;
                    --x;    
                }
            }
        }
        return sum;
    }
}
```
2257. Count Unguarded Cells in the Grid

You are given two integers m and n representing a 0-indexed m x n grid. You are also given two 2D integer arrays guards and walls where guards[i] = [rowi, coli] and walls[j] = [rowj, colj] represent the positions of the ith guard and jth wall respectively.

A guard can see every cell in the four cardinal directions (north, east, south, or west) starting from their position unless obstructed by a wall or another guard. A cell is guarded if there is at least one guard that can see it.

Return the number of unoccupied cells that are not guarded.

```
class Solution {
    public int countUnguarded(int m, int n, int[][] guards, int[][] walls) {
        int[][] grid = new int[m][n];
        
        // Mark guards and walls in the grid
        for (int[] guard : guards) {
            grid[guard[0]][guard[1]] = 1; // 1 represents a guard
        }
        for (int[] wall : walls) {
            grid[wall[0]][wall[1]] = 2; // 2 represents a wall
        }
        
        // Directions: north, east, south, west
        int[][] directions = {{-1, 0}, {0, 1}, {1, 0}, {0, -1}};
        
        // Mark cells that are guarded
        for (int[] guard : guards) {
            for (int[] dir : directions) {
                int x = guard[0];
                int y = guard[1];
                while (true) {
                    x += dir[0];
                    y += dir[1];
                    if (x < 0 || x >= m || y < 0 || y >= n || grid[x][y] == 1 || grid[x][y] == 2) {
                        break;
                    }
                    grid[x][y] = 3; // 3 represents a guarded cell
                }
            }
        }
        
        // Count unoccupied and unguarded cells
        int count = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 0) {
                    count++;
                }
            }
        }
        
        return count;
    }
}
```
1072. Flip Columns For Maximum Number of Equal Rows

You are given an m x n binary matrix matrix.

You can choose any number of columns in the matrix and flip every cell in that column (i.e., Change the value of the cell from 0 to 1 or vice versa).

Return the maximum number of rows that have all values equal after some number of flips.

 

Example 1:

Input: matrix = [[0,1],[1,1]]
Output: 1
Explanation: After flipping no values, 1 row has all values equal.

```
class Solution {
    public int maxEqualRowsAfterFlips(int[][] matrix) {
       Map<String, Integer> patternCount = new HashMap<>();
        
        for (int[] row : matrix) {
            StringBuilder pattern = new StringBuilder();
            StringBuilder complement = new StringBuilder();
            
            for (int cell : row) {
                pattern.append(cell);
                complement.append(1 - cell);
            }
            
            String patternStr = pattern.toString();
            String complementStr = complement.toString();
            
            patternCount.put(patternStr, patternCount.getOrDefault(patternStr, 0) + 1);
            patternCount.put(complementStr, patternCount.getOrDefault(complementStr, 0) + 1);
        }
        
        int maxRows = 0;
        for (int count : patternCount.values()) {
            maxRows = Math.max(maxRows, count);
        }
        
        return maxRows;  
    }
}
```
1861. Rotating the Box

You are given an m x n matrix of characters box representing a side-view of a box. Each cell of the box is one of the following:

A stone '#'
A stationary obstacle '*'
Empty '.'
The box is rotated 90 degrees clockwise, causing some of the stones to fall due to gravity. Each stone falls down until it lands on an obstacle, another stone, or the bottom of the box. Gravity does not affect the obstacles' positions, and the inertia from the box's rotation does not affect the stones' horizontal positions.

It is guaranteed that each stone in box rests on an obstacle, another stone, or the bottom of the box.

Return an n x m matrix representing the box after the rotation described above.

```
class Solution {
    public char[][] rotateTheBox(char[][] box) {
        int r = box.length;
        int c = box[0].length;

        char[][] rotated = new char[c][r];

        // Rotate the box 90 degrees clockwise
        for (int i = 0; i < r; i++) {
            for (int j = 0; j < c; j++) {
                rotated[j][r - 1 - i] = box[i][j];
            }
        }

        // Process the rotated box to simulate gravity
        for (int i = 0; i < c; i++) {
            for (int j = 0; j < r; j++) {
                if (rotated[i][j] == '.') {
                    int k = i;
                    while (k - 1 >= 0 && rotated[k - 1][j] == '#') {
                        rotated[k - 1][j] = '.';
                        rotated[k][j] = '#';
                        k--; // Move the index up to continue checking
                    }
                }
            }
        }

        return rotated;
    }
}
```
Maximum Matrix Sum
You are given an n x n integer matrix. You can do the following operation any number of times:

Choose any two adjacent elements of matrix and multiply each of them by -1.
Two elements are considered adjacent if and only if they share a border.

Your goal is to maximize the summation of the matrix's elements. Return the maximum sum of the matrix's elements using the operation mentioned above.

 

Example 1:


Input: matrix = [[1,-1],[-1,1]]
Output: 4
Explanation: We can follow the following steps to reach sum equals 4:
- Multiply the 2 elements in the first row by -1.
- Multiply the 2 elements in the first column by -1.
```
class Solution {
    public int maxMatrixSum(int[][] matrix) {
        int n = matrix.length;
        int negativeCount = 0;
        int minAbsValue = Integer.MAX_VALUE;
        int sum = 0;

        // Iterate through the matrix
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                int value = matrix[i][j];
                if (value < 0) {
                    negativeCount++;
                }
                sum += Math.abs(value);
                minAbsValue = Math.min(minAbsValue, Math.abs(value));
            }
        }

        // If the count of negative numbers is odd, subtract twice the smallest absolute value
        if (negativeCount % 2 != 0) {
            sum -= 2 * minAbsValue;
        }

        return sum;
    }
}
```
Sliding Puzzle

On an 2 x 3 board, there are five tiles labeled from 1 to 5, and an empty square represented by 0. A move consists of choosing 0 and a 4-directionally adjacent number and swapping it.

The state of the board is solved if and only if the board is [[1,2,3],[4,5,0]].

Given the puzzle board board, return the least number of moves required so that the state of the board is solved. If it is impossible for the state of the board to be solved, return -1.

 

Example 1:


Input: board = [[1,2,3],[4,0,5]]
Output: 1
Explanation: Swap the 0 and the 5 in one move.

```
import java.util.*;

public class Solution {
    public int slidingPuzzle(int[][] board) {
        String target = "123450";
        StringBuilder start = new StringBuilder();
        for (int[] row : board) {
            for (int num : row) {
                start.append(num);
            }
        }
        
        Map<Integer, List<Integer>> neighbors = new HashMap<>();
        neighbors.put(0, Arrays.asList(1, 3));
        neighbors.put(1, Arrays.asList(0, 2, 4));
        neighbors.put(2, Arrays.asList(1, 5));
        neighbors.put(3, Arrays.asList(0, 4));
        neighbors.put(4, Arrays.asList(1, 3, 5));
        neighbors.put(5, Arrays.asList(2, 4));
        
        return bfs(start.toString(), target, neighbors);
    }
    
    private List<String> getNextStates(String state, Map<Integer, List<Integer>> neighbors) {
        int zeroIndex = state.indexOf('0');
        List<String> nextStates = new ArrayList<>();
        for (int neighbor : neighbors.get(zeroIndex)) {
            char[] newState = state.toCharArray();
            newState[zeroIndex] = newState[neighbor];
            newState[neighbor] = '0';
            nextStates.add(new String(newState));
        }
        return nextStates;
    }
    
    private int bfs(String start, String target, Map<Integer, List<Integer>> neighbors) {
        Queue<String> queue = new LinkedList<>();
        Set<String> visited = new HashSet<>();
        queue.offer(start);
        visited.add(start);
        int steps = 0;
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                String current = queue.poll();
                if (current.equals(target)) {
                    return steps;
                }
                for (String nextState : getNextStates(current, neighbors)) {
                    if (!visited.contains(nextState)) {
                        queue.offer(nextState);
                        visited.add(nextState);
                    }
                }
            }
            steps++;
        }
        return -1; // If the puzzle is unsolvable
    }
}
```
Subsets

Given an integer array nums of unique elements, return all possible 
subsets
 (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.

 

Example 1:

Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
Example 2:

Input: nums = [0]
Output: [[],[0]]

```
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        generatesubsets(0,nums,new ArrayList<>(),result);
        return result;
    }

    private void generatesubsets(int index,int[] nums, List<Integer> current, List<List<Integer>> result){
        // add the new subset
        result.add(new ArrayList<>(current));
        for(int i = index;i<nums.length;i++){
            //create the new subset
            current.add(nums[i]);
            generatesubsets(i+1,nums,current,result);
            // remove the duplicate to proceed further addition.
            current.remove(current.size() - 1);
        }
    }
}
```
2097. Valid Arrangement of Pairs

You are given a 0-indexed 2D integer array pairs where pairs[i] = [starti, endi]. An arrangement of pairs is valid if for every index i where 1 <= i < pairs.length, we have endi-1 == starti.

Return any valid arrangement of pairs.

Note: The inputs will be generated such that there exists a valid arrangement of pairs.

 

Example 1:

Input: pairs = [[5,1],[4,5],[11,9],[9,4]]
Output: [[11,9],[9,4],[4,5],[5,1]]
Explanation:
This is a valid arrangement since endi-1 always equals starti.
end0 = 9 == 9 = start1 
end1 = 4 == 4 = start2
end2 = 5 == 5 = start3

```
import java.util.*;

public class Solution {
    public int[][] validArrangement(int[][] pairs) {
        Map<Integer, List<Integer>> graph = new HashMap<>();
        Map<Integer, Integer> inDegree = new HashMap<>();
        Map<Integer, Integer> outDegree = new HashMap<>();
        
        // Build the graph and count in-degrees and out-degrees
        for (int[] pair : pairs) {
            int start = pair[0];
            int end = pair[1];
            graph.computeIfAbsent(start, k -> new ArrayList<>()).add(end);
            outDegree.put(start, outDegree.getOrDefault(start, 0) + 1);
            inDegree.put(end, inDegree.getOrDefault(end, 0) + 1);
        }
        
        // Find the starting node
        int startNode = pairs[0][0];
        for (int node : outDegree.keySet()) {
            if (outDegree.get(node) - inDegree.getOrDefault(node, 0) == 1) {
                startNode = node;
                break;
            }
        }
        
        // Perform DFS to find the Eulerian path
        List<int[]> result = new ArrayList<>();
        Deque<Integer> stack = new ArrayDeque<>();
        stack.push(startNode);
        
        while (!stack.isEmpty()) {
            int node = stack.peek();
            if (graph.containsKey(node) && !graph.get(node).isEmpty()) {
                stack.push(graph.get(node).remove(graph.get(node).size() - 1));
            } else {
                stack.pop();
                if (!stack.isEmpty()) {
                    result.add(new int[]{stack.peek(), node});
                }
            }
        }
        
        // Convert the result list to array
        Collections.reverse(result);
        return result.toArray(new int[result.size()][]);
    }
}
```
1346. Check If N and Its Double Exist

Given an array arr of integers, check if there exist two indices i and j such that :

i != j
0 <= i, j < arr.length
arr[i] == 2 * arr[j]
 

Example 1:

Input: arr = [10,2,5,3]
Output: true
Explanation: For i = 0 and j = 2, arr[i] == 10 == 2 * 5 == 2 * arr[j]
Example 2:

Input: arr = [3,1,7,11]
Output: false
Explanation: There is no i and j that satisfy the conditions.

```
class Solution {
    public boolean checkIfExist(int[] arr) {
        int n = arr.length;
        for (int i = 0; i < n ;i++){
            for(int j = 0 ; j<n ; j++){
                if (j== i){
                    continue;
                }
                if(arr[i] == arr[j] * 2){
                    return true;
                }
            }
        }
        return false;
    }
}
```
1455. Check If a Word Occurs As a Prefix of Any Word in a Sentence

Given a sentence that consists of some words separated by a single space, and a searchWord, check if searchWord is a prefix of any word in sentence.

Return the index of the word in sentence (1-indexed) where searchWord is a prefix of this word. If searchWord is a prefix of more than one word, return the index of the first word (minimum index). If there is no such word return -1.

A prefix of a string s is any leading contiguous substring of s.

 

Example 1:

Input: sentence = "i love eating burger", searchWord = "burg"
Output: 4
Explanation: "burg" is prefix of "burger" which is the 4th word in the sentence.

```
/**
 * @param {string} sentence
 * @param {string} searchWord
 * @return {number}
 */
var isPrefixOfWord = function(sentence, searchWord) {
    const words = sentence.split(' ');
    for (let i = 0;i< words.length;i++){
        console.log(words[i].indexOf(searchWord));
        if(words[i].indexOf(searchWord) !== -1){
            if(words[i].substring(0,searchWord.length) === searchWord){
                return i + 1;
            }
        }
    }
    return -1;
};

```

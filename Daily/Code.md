Medium - 14/10/2024

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

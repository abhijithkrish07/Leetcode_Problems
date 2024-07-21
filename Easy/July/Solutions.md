Question.
Given an array of integers nums, calculate the pivot index of this array.

The pivot index is the index where the sum of all the numbers strictly to the left of the index is equal to the sum of all the numbers strictly to the index's right.

If the index is on the left edge of the array, then the left sum is 0 because there are no elements to the left. This also applies to the right edge of the array.

Return the leftmost pivot index. If no such index exists, return -1.


Example 1:

Input: nums = [1,7,3,6,5,6]
Output: 3
Explanation:
The pivot index is 3.
Left sum = nums[0] + nums[1] + nums[2] = 1 + 7 + 3 = 11
Right sum = nums[4] + nums[5] = 5 + 6 = 11

```
function findSum(nums: number[]): number {
    return nums.reduce((acc, cur) => {return acc+cur}, 0);
}
function pivotIndex(nums: number[]): number {
    const arrayLength = nums.length;
    for(let i = 0; i< arrayLength; i++){
        if(findSum(nums.slice(0,i)) === findSum(nums.slice(i+1,arrayLength))){
            return i;
        }
    }
    return -1;
};
```
Improvised Solution:
```
function pivotIndex(nums: number[]): number {
    const arrayLength = nums.length;
    let sum = 0;
    for(let i = 0; i< arrayLength; i++){
        sum+= nums[i];
    }
    let lSum = 0;
    for(let i = 0; i< arrayLength; i++){
        // why x2? If it really needs to left side equal right side, then
        // at the pivot,the left side must be equal to the sum/2 or sum
        // will be equal to lsumx2 
        // subtract that index because, so it's purely left and right equating
        if(lSum *2 === sum - nums[i]){
            return i;
        }
        lSum+= nums[i]
    }
    return -1;
    
};
```

July 18:

Question:

Given two 0-indexed integer arrays nums1 and nums2, return a list answer of size 2 where:

answer[0] is a list of all distinct integers in nums1 which are not present in nums2.
answer[1] is a list of all distinct integers in nums2 which are not present in nums1.
Note that the integers in the lists may be returned in any order.

 

Example 1:

Input: nums1 = [1,2,3], nums2 = [2,4,6]
Output: [[1,3],[4,6]]
Explanation:
For nums1, nums1[1] = 2 is present at index 0 of nums2, whereas nums1[0] = 1 and nums1[2] = 3 are not present in nums2. Therefore, answer[0] = [1,3].
For nums2, nums2[0] = 2 is present at index 1 of nums1, whereas nums2[1] = 4 and nums2[2] = 6 are not present in nums2. Therefore, answer[1] = [4,6].


Solution:
```
function findDifference(nums1: number[], nums2: number[]): number[][] {
  const res1= new Set<number>;
  const res2= new Set<number>;
  for(let i= 0; i< nums1.length; i++){
    if(nums2.indexOf(nums1[i]) === -1){
        res1.add(nums1[i]);
    }
  }

  for(let i= 0; i< nums2.length; i++){
    if(nums1.indexOf(nums2[i])  === -1){
        res2.add(nums2[i]);
    }
  }

  return[Array.from(res1),Array.from(res2)]
};
```

Question.

There is a biker going on a road trip. The road trip consists of n + 1 points at different altitudes. The biker starts his trip on point 0 with altitude equal 0.

You are given an integer array gain of length n where gain[i] is the net gain in altitude between points i​​​​​​ and i + 1 for all (0 <= i < n). Return the highest altitude of a point.

 

Example 1:

Input: gain = [-5,1,5,0,-7]
Output: 1
Explanation: The altitudes are [0,-5,-4,1,1,-6]. The highest is 1.
Example 2:

Input: gain = [-4,-3,-2,-1,4,3,2]
Output: 0
Explanation: The altitudes are [0,-4,-7,-9,-10,-6,-3,-1]. The highest is 0.

Solution:
```
function largestAltitude(gain: number[]): number {
    gain.unshift(0);
    let res = [0];
    for(let i=1;i<gain.length; i++){
        res[i] = res[i-1] + gain[i];
    }
    // since the .sort() converts the number to string and compares.Better to pass a compare function
    return res.sort((val1,val2) => val1 -val2)[res.length - 1];
};

```
Question:

Given an array of integers arr, return true if the number of occurrences of each value in the array is unique or false otherwise.

 

Example 1:

Input: arr = [1,2,2,1,1,3]
Output: true
Explanation: The value 1 has 3 occurrences, 2 has 2 and 3 has 1. No two values have the same number of occurrences.
Example 2:

Input: arr = [1,2]
Output: false
Example 3:

Input: arr = [-3,0,1,-3,1,1,1,-3,10,0]
Output: true

Solution:
```
function uniqueOccurrences(arr: number[]): boolean {
    const uniqueValues = new Map();
    arr.map(val => {
        if (uniqueValues.has(val)) {
            const existingCount = uniqueValues.get(val);
            uniqueValues.set(val, existingCount + 1)
        } else {

            uniqueValues.set(val, 1)
        }
    });
    if((new Set(Array.from(uniqueValues.values())).size) === uniqueValues.size){
        return true;
    }
    return false
};

```
Question:

You are given an integer array nums consisting of n elements, and an integer k.

Find a contiguous subarray whose length is equal to k that has the maximum average value and return this value. Any answer with a calculation error less than 10-5 will be accepted.

 

Example 1:

Input: nums = [1,12,-5,-6,50,3], k = 4
Output: 12.75000
Explanation: Maximum average is (12 - 5 - 6 + 50) / 4 = 51 / 4 = 12.75
Example 2:

Input: nums = [5], k = 1
Output: 5.00000

Answer: Solution is good, but time limit exceeds for larger input
```
function findMaxAverage(nums: number[], k: number): number {
    if(nums.length < Math.pow(10,5)){
        let maxAvgSum = Number.MIN_SAFE_INTEGER;
    for(let i=0;i+k<=nums.length; i++){
        const avgSum = (nums.slice(i,i+k).reduce(((a,b) => a+b), 0) )/ k;
        if(maxAvgSum < avgSum){
            maxAvgSum = avgSum;
        }
    }
    return maxAvgSum;
    }
};
```
Solution for all datasets with a different approach
```
function findMaxAverage(nums: number[], k: number): number {
    let windowSum = 0;
    let maxSum = Number.MIN_SAFE_INTEGER;
    //getting the first window sum
    for(let i = 0; i<k ;i++){
        windowSum+= nums[i]
    }
    maxSum = windowSum;
    // now moving on to finding the maxSum
    for(let i = k; i< nums.length; i++){
        //moving the window,
        // [1,2,3,4] is the array and if k is 2
        // first sum will be [1,2] then I'm adding 3 to sum and subtracting
        // 1 from the sum
        windowSum += nums[i] - nums[i - k]
        // And then finding the max of the window to that of maxSum
        maxSum = Math.max(windowSum, maxSum);
    }
    return maxSum/k;

};
```

Question:
206. Reverse Linked List

Solution
```
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function reverseList(head: ListNode | null): ListNode | null {
    let prev = null;
    let current = head;
    let next = null;

    while (current != null) {
        // take 1 , 2 , 3
        // take example of 2 and 3 link

        // store the next node to move further
        // next.val = 3 next.next = 4 
        next = current.next;

        // reversing the list
        // current.next = 1    
        current.next = prev;

        //below two steps is to move forward
        // prev.val = 2 prev.next = 3
        prev = current
        // current.val = 3 current.next = 4
        current = next;
    }
    return prev;
};
```
Question:
872. Leaf-Similar Trees

Input: root1 = [3,5,1,6,2,9,8,null,null,7,4], root2 = [3,5,1,6,7,4,2,null,null,null,null,null,null,9,8]
Output: true

```
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function leafVals(root: TreeNode | null, leaf: number[]) {
    if (root == null)
        return ;
    leafVals(root.left, leaf);
    if(root.left === null && root.right === null){
        leaf.push(root.val)
    }
    leafVals(root.right, leaf);
}

function leafSimilar(root1: TreeNode | null, root2: TreeNode | null): boolean {
    const leaf1 = [];
    const leaf2 = [];

    leafVals(root1, leaf1);
    leafVals(root2, leaf2);

    if(leaf1.length !== leaf2.length){
        return false
    }

    for(let i = 0; i< leaf1.length;i ++){
        if(leaf1[i]!= leaf2[i])
            return false;
    }

    return true
};
```
Question:
104. Maximum Depth of Binary Tree

A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

Eg1:
Input: root = [3,9,20,null,null,15,7]
Output: 3
Example 2:

Input: root = [1,null,2]
Output: 2

Code
```
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

    function dfs(node: TreeNode | null): number {
        if (!node) {
            return 0;
        }
        let left = dfs(node.left);
        let right = dfs(node.right);
        return Math.max(left, right) + 1;
    }


function maxDepth(root: TreeNode | null): number {
    return dfs(root);
};
```

338. Counting Bits

Given an integer n, return an array ans of length n + 1 such that for each i (0 <= i <= n), ans[i] is the number of 1's in the binary representation of i.

 

Example 1:

Input: n = 2
Output: [0,1,1]
Explanation:
0 --> 0
1 --> 1
2 --> 10
Example 2:

Input: n = 5
Output: [0,1,1,2,1,2]
Explanation:
0 --> 0
1 --> 1
2 --> 10
3 --> 11
4 --> 100
5 --> 101

Solution using JS in-built functions:
```
function countOnes(bin: string): number{
    let counter = 0;
    bin.split('').forEach(s=>{
        if(s === '1'){
            ++counter;
        }
    });
    return counter;
}

function countBits(n: number): number[] {
    const numArr = [];

    for(let i = 0;i<= n;i++){
        numArr.push(countOnes(i.toString(2)));
    }
    return numArr;
};
```

Optimal Solution:
```
function countBits(n: number): number[] {
    const numArr = new Array(n+1).fill(0);
    // we are starting from 1st position
    for (let i = 1; i <= n; i++) {
        // i>> 1 => means pushing 1 bit to the right
        // basically means to divide by 2
        // i & 1 checks the least significant bit
        // odd & 1 => 1
        // even & 1 => 0
      // numArr(1) = numArr(0) +  1.   => 1
        numArr[i] = numArr[i>>1] + (i&1);
    }
    return numArr;
};
```

Question:
136. Single Number

Given a non-empty array of integers nums, every element appears twice except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

 

Example 1:

Input: nums = [2,2,1]
Output: 1
Example 2:

Input: nums = [4,1,2,1,2]
Output: 4
Example 3:

Input: nums = [1]
Output: 1

Code:
```
function singleNumber(nums: number[]): number {
    let result = 0;
    for (let num of nums) {
        // ^= means XOR, why they go for XOR?
        // because in XOR, equal numbers get cancelled out
        // 1 and 0 => 1 , 1 and 1 => 0
        // so try do a bitwise calculation of XOR
        // the output of result would be
        // 4, 0 => 4
        // 4, 1 => 5
        // 5, 2 => 7
        // 7, 1 => 6 => it reduced
        // 6, 2 => 4
        result ^= num;
    }
    return result;
};
```
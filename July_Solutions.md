July 17
Easy : 

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

A.

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

Improvised Solution:

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

function largestAltitude(gain: number[]): number {
    gain.unshift(0);
    let res = [0];
    for(let i=1;i<gain.length; i++){
        res[i] = res[i-1] + gain[i];
    }
    // since the .sort() converts the number to string and compares.Better to pass a compare function
    return res.sort((val1,val2) => val1 -val2)[res.length - 1];
};

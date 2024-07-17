July 17
Easy : 

Q.
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

1796. Second Largest Digit in a String

Given an alphanumeric string s, return the second largest numerical digit that appears in s, or -1 if it does not exist.

An alphanumeric string is a string consisting of lowercase English letters and digits.

 

Example 1:

Input: s = "dfa12321afd"
Output: 2
Explanation: The digits that appear in s are [1, 2, 3]. The second largest digit is 2.
Example 2:

Input: s = "abc1111"
Output: -1
Explanation: The digits that appear in s are [1]. There is no second largest digit. 

Code:

```
function secondHighest(s: string): number {
    let pattern = /\d/g;
    
    const finalArr = s.match(pattern);
    
    if(finalArr == null || finalArr.length === 0){
        return -1;
    }

    let largest = Number(finalArr[0]);
    let second = -1;
    
    for(let i= 0; i< finalArr.length; i++){
        const newNum = Number(finalArr[i]);
        if(newNum>largest){
            second = largest;
            largest = newNum;
        } else if(newNum>second && newNum !== largest){
            second = newNum;
        }
    }
    
    
    return second;
};
```
1752. Check if Array Is Sorted and Rotated

Given an array nums, return true if the array was originally sorted in non-decreasing order, then rotated some number of positions (including zero). Otherwise, return false.

There may be duplicates in the original array.

Note: An array A rotated by x positions results in an array B of the same length such that A[i] == B[(i+x) % A.length], where % is the modulo operation.

 

Example 1:

Input: nums = [3,4,5,1,2]
Output: true
Explanation: [1,2,3,4,5] is the original sorted array.
You can rotate the array by x = 3 positions to begin on the the element of value 3: [3,4,5,1,2].
Example 2:

Input: nums = [2,1,3,4]
Output: false
Explanation: There is no sorted array once rotated that can make nums.
Example 3:

Input: nums = [1,2,3]
Output: true
Explanation: [1,2,3] is the original sorted array.
You can rotate the array by x = 0 positions (i.e. no rotation) to make nums.


Code:

```
function checkAscending(nums: number[]): boolean {
    for (let i = 1; i < nums.length; i++) {
        if (nums[i] >= nums[i - 1]) {
            continue;
        } else {
            return false;
        }
    }
    return true;
}
function check(nums: number[]): boolean {
    let flag = true;
    let lastDigit = Number.MIN_SAFE_INTEGER;
    for (let i = 1; i < nums.length; i++) {
        if (nums[i] >= nums[i - 1]) {
            continue;
        } else {
            let ind = nums.indexOf(lastDigit);
            if (lastDigit > nums[ind + 1]) {
                return false;
            } else {
                lastDigit = nums.pop();
                nums.unshift(lastDigit);
                const flag = checkAscending(nums);
                if (flag) {
                    return flag;
                }
            }
            i = 0;
        }
    }
    return flag;
};
```

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

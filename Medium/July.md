Question:
1448. Count Good Nodes in Binary Tree

Given a binary tree root, a node X in the tree is named good if in the path from root to X there are no nodes with a value greater than X.

Return the number of good nodes in the binary tree.
 

Example 1:
<br> <img width="744" alt="image" src="https://github.com/user-attachments/assets/e0a1236c-87a1-471a-971d-24188f500551"> <br>



Input: root = [3,1,4,3,null,1,5]
Output: 4
Explanation: Nodes in blue are good.
Root Node (3) is always a good node.
Node 4 -> (3,4) is the maximum value in the path starting from the root.
Node 5 -> (3,4,5) is the maximum value in the path
Node 3 -> (3,1,3) is the maximum value in the path.

Code:
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

function dfs(node: TreeNode | null, maxNumSoFar: number): number {
    if(!node){
        return 0;
    }
    let result = node.val >= maxNumSoFar ? 1 : 0;
    result += dfs(node.left, Math.max(node.val, maxNumSoFar));
    result += dfs(node.right, Math.max(node.val, maxNumSoFar));
    return result;
}



function goodNodes(root: TreeNode | null): number {
    return dfs(root, Number.MIN_SAFE_INTEGER);
};
```

450. Delete Node in a BST

Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return the root node reference (possibly updated) of the BST.

Basically, the deletion can be divided into two stages:

Search for a node to remove.
If the node is found, delete the node.
 

<br> <img width="805" alt="image" src="https://github.com/user-attachments/assets/9bdba321-eedb-495a-987a-0d275a614cce"> <br>

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

function deleteNode(root: TreeNode | null, val: number): TreeNode | null {
    if(!root){
        return null;
    }
    if(val< root.val){
        root.left = deleteNode(root.left,val);
    } else if(val > root.val){
        root.right = deleteNode(root.right,val);
    } else {
        if(!root.left)
            return root.right;
        if(!root.right)
            return root.left;
        
        root.val = minValue(root.right);
        root.right = deleteNode(root.right,root.val)
    }
    return root;
};

function minValue(node: TreeNode): number{
    let minVal = node.val;
    while(node.left!=null){
        minVal = node.left.val;
        node = node.left
    }
    return minVal;
}
```

1456. Maximum Number of Vowels in a Substring of Given Length

Given a string s and an integer k, return the maximum number of vowel letters in any substring of s with length k.

Vowel letters in English are 'a', 'e', 'i', 'o', and 'u'.

 
Example 1:

Input: s = "abciiidef", k = 3
Output: 3
Explanation: The substring "iii" contains 3 vowel letters.
Example 2:

Input: s = "aeiou", k = 2
Output: 2
Explanation: Any substring of length 2 contains 2 vowels.
Example 3:

Input: s = "leetcode", k = 3
Output: 2
Explanation: "lee", "eet" and "ode" contain 2 vowels.


Code:

```
function maxVowels(s: string, k: number): number {
    const vowels = ['a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'];  
    const vArr = s.split('').map(val => vowels.includes(val) ? 1 : 0);
    let windowSum = 0;
    for(let i = 0;i< k;i++){
        windowSum+=vArr[i];
    }
    let maxCount = windowSum
    for(let i =k;i<vArr.length;i++){
        windowSum+= vArr[i] - vArr[i-k];
        maxCount = Math.max(windowSum,maxCount);
    }
    return maxCount;
};
```

2390. Removing Stars From a String

You are given a string s, which contains stars *.

In one operation, you can:

Choose a star in s.
Remove the closest non-star character to its left, as well as remove the star itself.
Return the string after all stars have been removed.

Note:

The input will be generated such that the operation is always possible.
It can be shown that the resulting string will always be unique.
 

Example 1:

Input: s = "leet**cod*e"
Output: "lecoe"
Explanation: Performing the removals from left to right:
- The closest character to the 1st star is 't' in "leet**cod*e". s becomes "lee*cod*e".
- The closest character to the 2nd star is 'e' in "lee*cod*e". s becomes "lecod*e".
- The closest character to the 3rd star is 'd' in "lecod*e". s becomes "lecoe".
There are no more stars, so we return "lecoe".
Example 2:

Input: s = "erase*****"
Output: ""
Explanation: The entire string is removed, so we return an empty string.

Code
```
function removeStars(s: string): string {
    const res = [];
    for(let i= 0;i< s.length; i++){
        if(s.charAt(i) === '*'){
            res.pop();
        } else {
            res.push(s.charAt(i));
        }
    }
    return res.join('');
};
```
Given 3 positives numbers a, b and c. Return the minimum flips required in some bits of a and b to make ( a OR b == c ). (bitwise OR operation).
Flip operation consists of change any single bit 1 to 0 or change the bit 0 to 1 in their binary representation.

 
Example 1:


Input: a = 2, b = 6, c = 5
<br> <img width="653" alt="image" src="https://github.com/user-attachments/assets/44be71fe-419c-4aeb-b034-740eba770ae3"> <br>

Output: 3
Explanation: After flips a = 1 , b = 4 , c = 5 such that (a OR b == c)
Example 2:

Input: a = 4, b = 2, c = 7
Output: 1
Example 3:

Input: a = 1, b = 2, c = 3
Output: 0

```
function minFlips(a: number, b: number, c: number): number {
    let flips = 0;
    while (a > 0 || b > 0 || c > 0) {
        let bit_a = a & 1;
        let bit_b = b & 1;
        let bit_c = c & 1;
        if (bit_c === 0) {
            flips += bit_a + bit_b;
        } else {
            flips += 1 - (bit_a | bit_b);
        }
        a >>= 1
        b >>= 1
        c >>= 1
    }
    return flips;
};
```
735. Asteroid Collision

We are given an array asteroids of integers representing asteroids in a row.

For each asteroid, the absolute value represents its size, and the sign represents its direction (positive meaning right, negative meaning left). Each asteroid moves at the same speed.

Find out the state of the asteroids after all collisions. If two asteroids meet, the smaller one will explode. If both are the same size, both will explode. Two asteroids moving in the same direction will never meet.

 

Example 1:

Input: asteroids = [5,10,-5]
Output: [5,10]
Explanation: The 10 and -5 collide resulting in 10. The 5 and 10 never collide.
Example 2:

Input: asteroids = [8,-8]
Output: []
Explanation: The 8 and -8 collide exploding each other.
Example 3:

Input: asteroids = [10,2,-5]
Output: [10]
Explanation: The 2 and -5 collide resulting in -5. The 10 and -5 collide resulting in 10.

Code: 
Attempt 1 - 31/07 -> 199/270 Test cases passed

```
function asteroidCollision(asteroids: number[]): number[] {
    const numStack = [];
    for (let i = 0; i < asteroids.length; i++) {
        if (numStack.length === 0) {
            numStack.push(asteroids[i]);
        } else {
            let n = numStack.length - 1;
            if (numStack[n] < 0 && asteroids[i] > 0) {
                numStack.push(asteroids[i]);

            }
            if (asteroids[i] > 0 && numStack[n] > 0) {
                numStack.push(asteroids[i]);
            } else if (asteroids[i] < 0 && numStack[n] < 0) {
                numStack.push(asteroids[i]);
            } else if (numStack[n] > 0) {
                while (Math.abs(asteroids[i]) >= numStack[n] && numStack[n] > 0) {
                    numStack.pop();
                    --n;
                }
            }
        }
    }
    return numStack;
};
```

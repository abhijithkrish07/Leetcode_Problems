Question:
1448. Count Good Nodes in Binary Tree

Given a binary tree root, a node X in the tree is named good if in the path from root to X there are no nodes with a value greater than X.

Return the number of good nodes in the binary tree.
 

Example 1:
<img width="744" alt="image" src="https://github.com/user-attachments/assets/e0a1236c-87a1-471a-971d-24188f500551">
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

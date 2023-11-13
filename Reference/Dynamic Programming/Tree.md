# Tree Dynamic Programming
## Diameter of Binary Tree
Review: The largest depth of binary tree  
depth = max(`depth of let subtree`, `depth of right subtree`) + 1  

Example: [687. Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/description/)  
diameter of current node: `longest chain of left subtree` + `longest right chain of right subtree` + 2     
value return to parent node: max(`longest chain of left subtree`, `longest right chain of right subtree`) + 1   

### Binary Tree Maximum Path Sum
Example: [1617. Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/description/)   
path sum of current node: `maximum path sum of left subtree` + `maximum path sum of right subtree` + `value of current node`
value return to parent node: max(max(`longest chain of left subtree`, `longest right chain of right subtree`) + `value of current node`, 0)

### Longest Path with Different Adjacent Characters
Example: [2246. Longest Path with Different Adjacent Characters](https://leetcode.com/problems/longest-path-with-different-adjacent-characters/description/)  

## Maximum Independent Set on Trees(MIS)
MIS: Try to select nodes as many as possible, and ensure them non-adjacent.
### Binary Tree
Example: [337. House Robber III](https://leetcode.com/problems/house-robber-iii/description/)  
Select or Not:
1. Select current node: Neither left nor right node can be selected.
2. Not select current node: Left or right node can be either selected or not selected.

State:
1. Select current node: the maximum sum of the subtrees of current node.
2. Not select current node: the maximum sum of the subtrees of current node.

State Transition Function：
1. Select = `not select left` + `not select right` +  `current node value`
2. Not Select = max(`not select left`, `select left`) + max(`not select right`, `select right`)

Final answer: max(`select root`, `not select root`)  

### General Tree
Example: [P1352](https://www.luogu.com.cn/problem/P1352)  
State Transition Function：
1. Select = Σ(`not select`) + `current node value`
2. Not Select = Σmax(`not select`, `select`)

### How to Solve Tree DP
The relationship of tree and subtree is similar with the relationship of question and sub question.  

Frequent Methods:
1. Select or not.
2. Enumerate which one to select.
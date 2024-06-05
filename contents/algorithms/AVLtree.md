# AVL trees
An AVL tree is a self balancing binary search tree. If you recall, a binary search tree is a tree where the items to the right of a parent node are larger than the parent node, and the ones to the left are smaller. The problem with this is that when we are inserting items in increasing or decreasing size order, the binary search tree will become unbalanced an essentially turn into a linked list. This would see time complexity of searching increased to O(n) in the worst case.   

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/4b817593-0ff6-410a-8971-61442954bb21)

AVL trees aim to overcome this weakness by balancing the tree, ensuring that the complexity of searching will always be O(log(n)).

## What is balanced?
A tree is considered balanced if it has a height of O(log(n)). In the case of AVL trees, a tree is considered balanced if the heights of their left and right subtrees differ by at most one. Since BST operations are dependent on the height of the tree, if we keep it balanced we will be able to perform insertion, deletion and lookup operations in O(log(n)) time in an AVL tree.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/00bc4f6b-816d-48cd-90b4-52ad4218464c)

## Rebalancing
AVL trees maintain balance by performing rotations whenever an insertion or deletion operation violates the balance property. Rotations move some of the elements of the tree around in order to restore balance. We define the *balance factor* of a node to be the difference between the heights of its left and right subtrees i.e

balance_factor(u) = height(u.left) - height(u.right)

where height(null) = 0. A tree is therefore imbalanced if there is a node *u* such that

balance_factor ≥ 2

There are four seperate cases that can occur when a tree is imbalanced

### Left-left imbalance
A left-left imbalance occurs when a node's balance factor is 2 and the balance factor of the left node is non-negative (i.e there are two left children). To remedy this imbalance we perform a right rotation.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/0162efa2-a141-4691-92c8-e64ff1d3ff0c)

A left-left imbalance and the resulting tree after the right rotation has been performed

#### Right rotation pseudocode
```
1: function ROTATE_RIGHT(root)
2:   par = root.parent
3:   pivot = root.left
4:   temp = pivot.right
5:   pivot.set_right_child(root)
6:   root.set_left_child(temp)
7:   par.swap_child(root, pivot)
```

### Right-right imbalance
A right-right imbalance occurs when a node's balance factor is -2 and the balance factor of the right node is non-positive (i.e there are two right children). To remedy this we perform a left rotation

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/bc7035ca-6f16-422b-89f1-35eb663c63ed)
![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/8b782099-9a9f-4248-838e-4da4c31d7c83)

A right-right imbalance and the resulting tree after the left rotation has been performed

#### Left rotation pseudocode
```
1: function ROTATE_LEFT(root)
2:   par = root.parent
3:   pivot = root.right
4:   temp = pivot.left
5:   pivot.set_left_child(root)
6:   root.set_right_child(temp)
7:   par.swap_child(root, pivot)
```

### Left-right imbalance
A left-right imbalance occurs when a node's balance factor is 2 and the balance factor of the left node is negative (i.e there is a left child, and that left child has a right child). We must perform a double-right rotation to balance it.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/b9638e11-106e-4665-8ae2-93bb43ae7ab0)

#### Double-right rotation pseudocode
```
1: function DOUBLE_ROTATE_RIGHT(root)
2:   rotate_left(root.left)
3:   rotate_right(root)
```

### Right-left imbalance
A right-left imbalance occurs when a nodes balance factor is -2 and the balance factor of the right node is positive (i.e there is a right child, and that right child has a left child). We must perform a double-left rotation to balance it.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/9ca76cea-4d87-498d-b56e-f69c324e218a)

#### Double-left rotation pseudocode
```
1: function DOUBLE_ROTATE_LEFT(root)
2:   rotate_right(root.right)
3:   rotate_left(root)
```

## Full rebalancing procedure
Combining all the above scenarios, we can create a full rebalance procedure that will perform the correct rotations depending on the type of imbalance.

```
1: function REBALANCE(node)
2:   if balance_factor(node) = 2 then
3:     if balance_factor(node.left) < 0 then
4:       DOUBLE_ROTATE_RIGHT(node)
5:     else
6:       ROTATE_RIGHT(node)
7:   else if balance_factor(node) = -2 then
8:     if balance_factor(node.right) > 0 then
9:       DOUBLE_ROTATE_LEFT(node)
10:    else
11:      ROTATE_LEFT(node)
```

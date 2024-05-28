**Insert:**

```java

TreeNode insertBST(TreeNode root, int val) {
  if (root == null) return new TreeNode(val);

  if (root.val > val) root.left = insertBST(root.left, val);
  if (root.val < val) root.right = insertBST(root.right, val);
  return root;
}

```

**Delete**

```java
TreeNode deleteBST(TreeNode root, int val) {
  if (root == null) return null;

  if (root.val == val) {
    if (root.left == null) return root.right;
    if (root.right == null) return root.left;

    TreeNode minNode = getMin(root.right);
    root.right = deleteBST(root.right, minNode.val);
    minNode.left = root.left;
    minNode.right = root.right;
    root = minNode;

  } else if (root.val > val) {
    root.left = deleteBST(root.left, val);
  } else if (root.val < val) {
    root.right = deleteBST(root.right, val);
  }
  return root;
}

TreeNode getMin(TreeNode root) {
  while (root.left != null) {
    root = root.left;
  }
  return root;
}

```

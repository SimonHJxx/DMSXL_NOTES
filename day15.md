### 110.平衡二叉树 （优先掌握递归）

- 递归调用，两个函数都递归，一个用于判断左右子树高度差并传入新的左右子树，另一个求出子树的高度

  ```
  /**
   * Definition for a binary tree node.
   * struct TreeNode {
   *     int val;
   *     struct TreeNode *left;
   *     struct TreeNode *right;
   * };
   */
  int getDepth(struct TreeNode* node) {
      if(node == NULL) {
          return 0;
      }
      int rightDepth = getDepth(node->right);
      int leftDepth = getDepth(node->left);
  
      return rightDepth > leftDepth ? rightDepth + 1 : leftDepth + 1;
  }
  
  bool isBalanced(struct TreeNode* root) {
      if (!root)
          return 1;
      int leftDepth = getDepth(root->left);
      int rightDepth = getDepth(root->right);
      int diff;
      if ((diff = leftDepth - rightDepth) > 1 || diff < -1)
          return 0;
      return isBalanced(root->left) && isBalanced(root->right);
  }
  ```

  

### 257. 二叉树的所有路径 （优先掌握递归）

- digui

  ```
  /**
   * Definition for a binary tree node.
   * struct TreeNode {
   *     int val;
   *     struct TreeNode *left;
   *     struct TreeNode *right;
   * };
   */
  /**
   * Note: The returned array must be malloced, assume caller calls free().
   */
  void construct_paths(struct TreeNode* root, char** paths, int* returnSize, int* sta, int top) {
      if (root != NULL) {
          if (root->left == NULL && root->right == NULL) {
              char* tmp = (char*)malloc(1001);
              int len = 0;
              for (int i = 0; i < top; i++){
                  len += sprintf(tmp + len, "%d->", sta[i]);
              }
              sprintf(tmp + len, "%d", root->val);
              paths[(*returnSize)++] = tmp;
          } else {
              sta[top++] = root->val;
              construct_paths(root->left, paths, returnSize, sta, top);
              construct_paths(root->right, paths, returnSize, sta, top);
          }
      }
  }
  
  char** binaryTreePaths(struct TreeNode* root, int* returnSize) {
      char** paths = (char**)malloc(sizeof(char*) * 1001);
      *returnSize = 0;
      int sta[1001];
      construct_paths(root, paths, returnSize, sta, 0);
      return paths;
  }
  ```
  
  

### 404.左叶子之和 （优先掌握递归）

- digui

  ```
  /**
   * Definition for a binary tree node.
   * struct TreeNode {
   *     int val;
   *     struct TreeNode *left;
   *     struct TreeNode *right;
   * };
   */
  
  
  int sumOfLeftLeaves(struct TreeNode* root){
      if (!root)
          return 0;
      int left = sumOfLeftLeaves(root->left);
      int right = sumOfLeftLeaves(root->right);
      int midValue = 0;
      if (root->left && !root->left->left && !root->left->right)
          midValue = root->left->val;
      return left + right + midValue;
  }
  ```

  

### 222.完全二叉树的节点个数（优先掌握递归）

- digui

  ```
  /**
   * Definition for a binary tree n ode.
   * struct TreeNode {
   *     int val;
   *     struct TreeNode *left;
   *     struct TreeNode *right;
   * };
   */
  int getNodes(struct TreeNode* root) {
      if (root == NULL)
          return 0;
      int leftCount = getNodes(root->left);
      int rightCount = getNodes(root->right);
      return leftCount + rightCount + 1;
  }
  
  int countNodes(struct TreeNode* root) {
      return getNodes(root);
  }
  ```

  
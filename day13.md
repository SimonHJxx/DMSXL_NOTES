### 理论基础


- 树

- 二叉树（满二叉树/完全二叉树）

- 堆（大根堆/小根堆）（堆排序）

- 二叉查找树

- 平衡二叉查找树

- 二叉树的遍历

  - 深度优先遍历：前序遍历，中序遍历，后序遍历
  
  - 广度优先遍历：层次遍历

- B树
  
  

### 递归遍历

- 

  ```
  // 前序遍历
  void preOrder(struct TreeNode* root, int* ret, int* returnSize) {
      if(root == NULL){
          return;
      }
      ret[(*returnSize)++] = root -> val;
      preOrder(root -> left, ret, returnSize);
      preOrder(root -> right, ret, returnSize);
  }
  
  int* preorderTraversal(struct TreeNode* root, int* returnSize) {
      int* ret = (int*)malloc(sizeof(int) * 100);
      *returnSize = 0;
      preOrder(root, ret, returnSize);
      return ret;
  }
  // 中序遍历
  void inOrder(struct TreeNode* root, int* ret, int* returnSize) {
      if(root == NULL){
          return;
      }
      inOrder(root -> left, ret, returnSize);
      ret[(*returnSize)++] = root -> val;
      inOrder(root -> right, ret, returnSize);
  }
  
  int* inorderTraversal(struct TreeNode* root, int* returnSize) {
      int* ret = (int*)malloc(sizeof(int) * 100);
      *returnSize = 0;
      inOrder(root, ret, returnSize);
      return ret;
  }
  
  // 后序遍历
  void postOrder(struct TreeNode* root, int* ret, int* returnSize) {
      if(root == NULL){
          return;
      }
      postOrder(root -> left, ret, returnSize);
      postOrder(root -> right, ret, returnSize);
      ret[(*returnSize)++] = root -> val;
  }
  
  int* postorderTraversal(struct TreeNode* root, int* returnSize) {
      int* ret = (int*)malloc(sizeof(int) * 100);
      *returnSize = 0;
      postOrder(root, ret, returnSize);
      return ret;
  }
  ```
  
  

### 迭代遍历

- 

  ```
  struct TreeNode{
      int val;
      struct TreeNode* left;
      struct TreeNode* right;
  };
  
  int sizeOfTree(struct TreeNode* root) {
      if(root == NULL)
          return 0;
      return sizeOfTree(root->left) + sizeOfTree(root->right) + 1;
  }
  
  int* preOrderTraversal(struct TreeNode* root, int* returnsize) {
      int len = sizeOfTree(root);
      int* ans = (int*)malloc(sizeof (int) * len);
      *returnsize = len;
      if (root == NULL)
          return ans;
      struct TreeNode** stack = (struct TreeNode**)malloc(sizeof(struct TreeNode*) * (len + 1));
      int top = 0;
      stack[top] = root;
      struct TreeNode* cur = NULL;
      int i = 0;
      while (top >= 0) {
          cur = stack[top--];
          ans[i++] = cur->val;
          if (cur->right != NULL)
              stack[++top] = cur->right;
          if (cur->left != NULL)
              stack[++top] = cur->left;
      }
      return ans;
  }
  
  int* inOrderTraversal(struct TreeNode* root, int* returnsize) {
      int len = sizeOfTree(root);
      int* ans = (int*)malloc(sizeof (int) * len);
      *returnsize = 0;
      if (len == 0)
          return ans;
      struct TreeNode** stack = (struct TreeNode**) malloc(sizeof(struct TreeNode*) * (len + 1));
      int top = 0;
      struct TreeNode* cur = root;
      while (top != 0 || cur != NULL) {
          while (cur != NULL) {
              stack[top++] = cur;
              cur = cur->left;
          }
          cur = stack[--top];
          ans[(*returnsize)++] = cur->val;
          cur = cur->right;
      }
      return ans;
  }
  
  int* inOrderTraversalIterative(struct TreeNode* root, int* returnsize) {
      int len = sizeOfTree(root);
      int* ans = (int*)malloc(sizeof (int) * len);
      *returnsize = 0;
      if (len == 0)
          return ans;
      struct TreeNode** stack = (struct TreeNode**)malloc(sizeof(struct TreeNode*) * (len + 1));
      int top = 0;
      struct TreeNode* cur = root;
      stack[top] = root;
      while (top != -1) {
          while (stack[top] != NULL) {
              stack[++top] = cur->left;
          }
          top--;
          if (top != -1) {
              cur = stack[top];
              ans[(*returnsize)++] = cur->val;
              stack[top] = cur->right;
          }
      }
      return ans;
  }
  
  int* postOrderTraversal(struct TreeNode* root, int* returnsize) {
      int len = sizeOfTree(root);
      *returnsize = len;
      int* ans = (int*)malloc(sizeof (int) * len);
      if (len == 0)
          return ans;
      struct TreeNode** stack = (struct TreeNode**)malloc(sizeof(struct TreeNode*) * (len + 1));
      int top = 0;
      struct TreeNode* cur = root;
      stack[top] = root;
      while (top != -1) {
          cur = stack[top--];
          ans[--len] = cur->val;
          if (cur->left != NULL)
              stack[++top] = cur->left;
          if (cur->right != NULL)
              stack[++top] = cur->right;
      }
      return ans;
  }
  
  
  ```

### 统一迭代

- 

### 层序遍历

- 

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
   * Return an array of arrays of size *returnSize.
   * The sizes of the arrays are returned as *returnColumnSizes array.
   * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
   */
  int** levelOrder(struct TreeNode* root, int* returnSize, int** returnColumnSizes) {
      if (root == NULL) {
          *returnSize = 0;
          *returnColumnSizes = NULL;
          return NULL;
      }
      // 二维数组中一维数组的数量
      *returnSize = 0;
      // 每个返回的二维数组中一维数组的元素个数
      *returnColumnSizes = (int*)malloc(sizeof(int) * 2001);
      // 初始化待返回的二维数组
      int** ans = (int**) malloc(sizeof(int*) * 2001);
      // 开辟队列空间
      struct TreeNode** queue = (struct TreeNode**) malloc(sizeof(struct TreeNode*) * 2001);
      // 既是每行的左右边界，又是队列的左右边界
      int left = 0, right = 0;
      queue[right++] = root;
      while (left < right){
          int len = right - left;
          int* arr = (int*) malloc(sizeof(int) * len);
          (*returnColumnSizes)[*returnSize] = len;
          for (int i = 0; i < len; ++i) {
              struct TreeNode* node = queue[left++];
              arr[i] = node -> val;
              if (node -> left) queue[right++] = node -> left;
              if (node -> right) queue[right++] = node -> right;
          }
          ans[(*returnSize)++] = arr;
  
      }
      return ans;
  }
  ```

  
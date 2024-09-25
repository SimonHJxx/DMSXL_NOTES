### 找树左下角的值

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
  void dfs(struct TreeNode* root, int height, int* curVal, int* curHeight) {
      if (root == NULL)
          return;
      height++;
      dfs(root->left, height, curVal, curHeight);
      dfs(root->right, height, curVal, curHeight);
      if (height > *curHeight) {
          *curHeight = height;
          *curVal = root->val;
      }
  }
  
  int findBottomLeftValue(struct TreeNode* root) {
      int curVal, curHeight = 0;
      dfs(root, 0, &curVal, &curHeight);
      return curVal;
  
  }
  
  /**
   * Definition for a binary tree node.
   * struct TreeNode {
   *     int val;
   *     struct TreeNode *left;
   *     struct TreeNode *right;
   * };
   */
  #define MAX_NODE_SIZE 10000
  
  int findBottomLeftValue(struct TreeNode* root) {
      int ret;
      struct TreeNode** queue = (struct TreeNode**)malloc(MAX_NODE_SIZE * sizeof(struct TreeNode*));
      int head = 0, tail = 0;
      queue[tail++] = root;
      while (head != tail) {
          struct TreeNode* p = queue[head++];
          if (p->right)
              queue[tail++] = p->right;
          if (p->left)
              queue[tail++] = p->left;
          ret = p->val;
      }
      free(queue);
      return ret;
  }
  ```

  

### 路径总和

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
  bool hasPathSum(struct TreeNode* root, int targetSum) {
      if (!root)
          return false;
      if (!root->left && !root->right && root->val == targetSum)
          return true;
      return hasPathSum(root->left, targetSum - root->val) || hasPathSum(root->right, targetSum - root->val);
  }
  ```

  

### 从中序与后序遍历序列构造二叉树 

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
  
  int linearSearch(int* arr, int arrSize, int key) {
      int i;
      for (i = 0; i < arrSize; i++) {
          if (arr[i] == key)
              return i;
      }
      return -1;
  }
  
  struct TreeNode* buildTree(int* inorder, int inorderSize, int* postorder, int postorderSize) {
      if(!inorderSize)
          return NULL;
      struct TreeNode* node = (struct TreeNode*)malloc(sizeof (struct TreeNode));
      node->val = postorder[postorderSize - 1];
      int index = linearSearch(inorder, inorderSize, postorder[postorderSize - 1]);
      int rightSize = inorderSize - index - 1;
      node->left = buildTree(inorder, index, postorder, index);
      node->right = buildTree(inorder + index + 1, rightSize, postorder + index, rightSize);
      return node;
  }
  ```

  
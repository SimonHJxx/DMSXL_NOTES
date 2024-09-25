### 669. 修剪二叉搜索树

- xas

  ```
  /**
   * Definition for a binary tree node.
   * struct TreeNode {
   *     int val;
   *     struct TreeNode *left;
   *     struct TreeNode *right;
   * };
   */
  struct TreeNode* trimBST(struct TreeNode* root, int low, int high) {
      if (root == NULL) {
          return NULL;
      }
      if (root->val < low) {
          return trimBST(root->right, low, high);
      }
      else if (root->val > high) {
          return trimBST(root->left, low, high);
      }
      else {
          root->left = trimBST(root->left, low, high);
          root->right = trimBST(root->right, low, high);
          return root;
      }
  }
  ```

  

### 108.将有序数组转换为二叉搜索树

- dew

  ```
  /**
   * Definition for a binary tree node.
   * struct TreeNode {
   *     int val;
   *     struct TreeNode *left;
   *     struct TreeNode *right;
   * };
   */
  struct TreeNode* traversal(int* nums, int left, int right) {
      if (left > right)
          return NULL;
      int mid = left + ((right - left) / 2);
      struct TreeNode* root = (struct TreeNode*)malloc(sizeof(struct TreeNode));
      root->val = nums[mid];
      root->left = traversal(nums, left, mid - 1);
      root->right = traversal(nums, mid + 1, right);
      return root;
  }
  struct TreeNode* sortedArrayToBST(int* nums, int numsSize) {
      struct TreeNode* root = traversal(nums, 0, numsSize - 1);
      return root;
  }
  ```

  

### 538.把二叉搜索树转换为累加树

- wsd

  ```
  /**
   * Definition for a binary tree node.
   * struct TreeNode {
   *     int val;
   *     struct TreeNode *left;
   *     struct TreeNode *right;
   * };
   */
  
  int pre;
  void traverse(struct TreeNode* node) {
      if (node == NULL)
          return;
      traverse(node->right);
      node->val = node->val + pre;
      pre = node->val;
      traverse(node->left);
  }
  
  struct TreeNode* convertBST(struct TreeNode* root) {
      pre = 0;
      traverse(root);
      return root;
  }
  ```

  


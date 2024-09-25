### 654.最大二叉树

- qw

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
      if (left >= right)
          return NULL;
      int maxIndex = left;
      for (int i = left + 1; i < right; ++i) {
          if (nums[i] > nums[maxIndex])
              maxIndex = i;
      }
      
      struct TreeNode* node = (struct TreeNode*)malloc(sizeof(struct TreeNode));
      node->val = nums[maxIndex];
      node->left = traversal(nums, left, maxIndex);
      node->right = traversal(nums, maxIndex + 1, right);
      return node;
  }
  
  struct TreeNode* constructMaximumBinaryTree(int* nums, int numsSize) {
      return traversal(nums, 0, numsSize);
  }
  ```

  

### 617.合并二叉树

- as

  ```
  /**
   * Definition for a binary tree node.
   * struct TreeNode {
   *     int val;
   *     struct TreeNode *left;
   *     struct TreeNode *right;
   * };
   */
  struct TreeNode* mergeTrees(struct TreeNode* root1, struct TreeNode* root2) {
      if (root1 == NULL)
          return root2;
      if (root2 == NULL)
          return root1;
      struct TreeNode* merged = (struct TreeNode*)malloc(sizeof(struct TreeNode));
      merged->val = root1->val + root2->val;
      merged->left = mergeTrees(root1->left, root2->left);
      merged->right = mergeTrees(root1->right, root2->right);
      return merged;
  }
  ```

  

### 700.二叉搜索树中的搜索

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
  struct TreeNode* searchBST(struct TreeNode* root, int val) {
      if (root == NULL)
          return NULL;
      if (root->val == val)
          return root;
      if (val < root->val)
          return searchBST(root->left, val);
      else
          return searchBST(root->right, val);
  }
  ```

  

### 98.验证二叉搜索树

- dxw

  ```
  /**
   * Definition for a binary tree node.
   * struct TreeNode {
   *     int val;
   *     struct TreeNode *left;
   *     struct TreeNode *right;
   * };
   */
  int isBSTUtil(struct TreeNode* node, int min, int max) {
      if (node == NULL) {
          return 1;
      }
      if (node->val <= min || node->val >= max) {
          return 0;
      }
      return isBSTUtil(node->left, min, node->val) && isBSTUtil(node->right, node->val, max);
  }
  
  bool isValidBST(struct TreeNode* root) {
      return isBSTUtil(root, INT_MIN, INT_MAX);
  }
  ```

  
### 226.翻转二叉树 （优先掌握递归）

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
  struct TreeNode* invertTree(struct TreeNode* root) {
      if(root == NULL)
          return NULL;
      struct TreeNode* temp = root -> right;
      root -> right = root -> left;
      root -> left = temp;
      invertTree(root -> left);
      invertTree(root -> right);
      return root;
  }
  ```

  

### 101. 对称二叉树 （优先掌握递归）

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
   
  bool check(struct TreeNode* left, struct TreeNode* right) {
      if (left == NULL && right == NULL) {
          return true;
      }
      if (left == NULL || right == NULL) {
          return false;
      }
      if (left -> val  == right -> val) {
          return check(left -> left, right -> right) && check(left -> right, right -> left);
      } 
      else
          return false;
  }
  
  
  bool isSymmetric(struct TreeNode* root) {
      return check(root, root);
  }
  ```

  

### 104.二叉树的最大深度 （优先掌握递归）

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
  int maxDepth(struct TreeNode* root) {
      if (root == NULL) {
          return 0;
      }
      int left = maxDepth(root -> left);
      int right = maxDepth(root -> right);
      int max = left > right ? left : right;
      return max + 1;
  }
  ```

  

### 111.二叉树的最小深度 （优先掌握递归）

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
  int minDepth(struct TreeNode* root) {
      if (root == NULL){
          return 0;
      }
      if (root->left == NULL && root->right == NULL){
          return 1;
      }
      int min_depth = INT_MAX;
      if (root -> left != NULL){
          min_depth = fmin(minDepth(root->left), min_depth);
      }
      if (root -> right!= NULL){
          min_depth = fmin(minDepth(root->right), min_depth);
      }
      
      return min_depth + 1;
  }
  ```

  


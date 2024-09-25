### 235. 二叉搜索树的最近公共祖先

- da

  ```
  /**
   * Definition for a binary tree node.
   * struct TreeNode {
   *     int val;
   *     struct TreeNode *left;
   *     struct TreeNode *right;
   * };
   */
  
  struct TreeNode* lowestCommonAncestor(struct TreeNode* root, struct TreeNode* p, struct TreeNode* q) {
      struct TreeNode* ancestor = root;
      while (true) {
          if (p->val < ancestor->val && q->val < ancestor->val) 
              ancestor = ancestor->left;
          else if (p->val > ancestor->val && q->val > ancestor->val)
              ancestor = ancestor->right;
          else
              break;
      }
      return ancestor;
  }
  ```

  

### 701.二叉搜索树中的插入操作

- xsa

  ```
  /**
   * Definition for a binary tree node.
   * struct TreeNode {
   *     int val;
   *     struct TreeNode *left;
   *     struct TreeNode *right;
   * };
   */
  struct TreeNode* creatTreeNode(int val) {
      struct TreeNode* ret = (struct TreeNode*)malloc(sizeof(struct TreeNode));
      ret->val = val;
      ret->left = NULL;
      ret->right = NULL;
      return ret;
  }
  
  struct TreeNode* insertIntoBST(struct TreeNode* root, int val) {
      if (root == NULL) {
          root = creatTreeNode(val);
          return root;
      }
      struct TreeNode* pos = root;
      while (pos != NULL) {
          if (val < pos->val) {
              if (pos->left == NULL) {
                  pos->left = creatTreeNode(val);
                  break;
              }
              else {
                  pos = pos->left;
              }
          }
          else {
              if (pos->right == NULL) {
                  pos->right = creatTreeNode(val);
                  break;
              }
              else {
                  pos = pos->right;
              }
          }
      }
      return root;
  }
  ```

  

### 450.删除二叉搜索树中的节点

- dc

  ```
  /**
   * Definition for a binary tree node.
   * struct TreeNode {
   *     int val;
   *     struct TreeNode *left;
   *     struct TreeNode *right;
   * };
   */
  
  
  struct TreeNode* deleteNode(struct TreeNode* root, int key){
      if (root == NULL)
          return NULL;
      if (root->val > key) {
          root->left = deleteNode(root->left, key);
          return root;
      }
      if (root->val < key) {
          root->right = deleteNode(root->right, key);
          return root;
      }
      if (root->val == key) {
          if (!root->left && !root->right)
              return NULL;
          if (!root->right)
              return root->left;
          if (!root->left)
              return root->right;
          struct TreeNode* successor = root->right;
          while (successor->left) {
              successor = successor->left;
          }
          root->right = deleteNode(root->right, successor->val);
          successor->left = root->left;
          successor->right = root->right;
          return successor;
      }
      return root;
  }
  ```

  
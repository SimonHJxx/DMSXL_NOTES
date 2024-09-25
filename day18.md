### 530.二叉搜索树的最小绝对差

- a

  ```
  /**
   * Definition for a binary tree node.
   * struct TreeNode {
   *     int val;
   *     struct TreeNode *left;
   *     struct TreeNode *right;
   * };
   */
   void dfs(struct TreeNode* root, int* pre, int* ans) {
       if (root == NULL)
           return;
       dfs (root->left, pre, ans);
       if (*pre == -1)
           *pre = root->val;
       else {
           *ans = fmin(*ans, root->val - (*pre));
           *pre = root->val;
       }
          dfs (root->right, pre, ans);
   }
  
  int getMinimumDifference(struct TreeNode* root) {
      int ans = INT_MAX, pre = -1;
      dfs(root, &pre, &ans);
      return ans;
  }
  ```

  

### 501.二叉搜索树中的众数

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
  /**
   * Note: The returned array must be malloced, assume caller calls free().
   */
  int* answer;
  int answerSize;
  int base, count, maxCount;
  
  void update(int x) {
      if (x == base)
          ++count;
      else {
          count = 1;
          base = x;
      }
      if (count == maxCount)
          answer[answerSize++] = base;
      if (count > maxCount) {
          maxCount = count;
          answerSize = 0;
          answer[answerSize++] = base;
      }
  }
  
  void dfs(struct TreeNode* o) {
      if (o == NULL)
          return;
      dfs(o->left);
      update(o->val);
      dfs(o->right);
  }
  
  int* findMode(struct TreeNode* root, int* returnSize) {
      base = count = maxCount = 0;
      answer = malloc(sizeof(int) * 1000);
      answerSize = 0;
      dfs(root);
      *returnSize = answerSize;
      return answer;
  }
  ```

  

### 236. 二叉树的最近公共祖先

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
  struct TreeNode* lowestCommonAncestor(struct TreeNode* root, struct TreeNode* p, struct TreeNode* q) {
      if (root == NULL || root == p || root == q)
          return root;
      struct TreeNode* left = lowestCommonAncestor(root->left, p, q);
      struct TreeNode* right = lowestCommonAncestor(root->right, p, q);
      if (NULL != left && NULL != right)
          return root;
      return (NULL == left) ? right : left;
  }
  ```

  
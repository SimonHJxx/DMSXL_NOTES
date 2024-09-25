### 理论基础

```text
void backtracking(参数) {
    if (终止条件) {
        存放结果;
        return;
    }

    for (选择：本层集合中元素（树中节点孩子的数量就是集合的大小）) {
        处理节点;
        backtracking(路径，选择列表); // 递归
        回溯，撤销处理结果
    }
}
```

### 77. 组合

- cs

  ```
  /**
   * Return an array of arrays of size *returnSize.
   * The sizes of the arrays are returned as *returnColumnSizes array.
   * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
   */
  int* path;
  int pathTop;
  int** ans;
  int ansTop;
  
  void backTracking(int n, int k, int startIndex){
      if(pathTop == k) {
          int* tmp = (int*)malloc(sizeof(int) * k);
          for (int i = 0; i < k; i++) {
              tmp[i] = path[i];
          }
          ans[ansTop++] = tmp;
          return;
      }
      for (int j = startIndex; j <= n; j++) {
          path[pathTop++] = j;
          backTracking(n, k, j+1);
          pathTop--;
      }
  }
  
  int** combine(int n, int k, int* returnSize, int** returnColumnSizes) {
      path = (int*)malloc(sizeof(int) * k);
      ans = (int**)malloc(sizeof(int*) * 10000);
      pathTop = ansTop = 0;
  
      backTracking(n, k, 1);
      *returnSize = ansTop;
      *returnColumnSizes = (int*) malloc(sizeof(int) * (*returnSize));
      for (int i = 0; i < *returnSize; ++i) {
          (*returnColumnSizes)[i] = k;
      }
      return ans;
  
  }
  
  /**
   * Return an array of arrays of size *returnSize.
   * The sizes of the arrays are returned as *returnColumnSizes array.
   * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
   */
  int* path;
  int pathTop;
  int** ans;
  int ansTop;
  
  void backTracking(int n, int k, int startIndex){
      if(pathTop == k) {
          int* tmp = (int*)malloc(sizeof(int) * k);
          for (int i = 0; i < k; i++) {
              tmp[i] = path[i];
          }
          ans[ansTop++] = tmp;
          return;
      }
      for (int j = startIndex; j <= n - (k - pathTop) + 1; j++) {
          path[pathTop++] = j;
          backTracking(n, k, j+1);
          pathTop--;
      }
  }
  
  int** combine(int n, int k, int* returnSize, int** returnColumnSizes) {
      path = (int*)malloc(sizeof(int) * k);
      ans = (int**)malloc(sizeof(int*) * 10000);
      pathTop = ansTop = 0;
  
      backTracking(n, k, 1);
      *returnSize = ansTop;
      *returnColumnSizes = (int*) malloc(sizeof(int) * (*returnSize));
      for (int i = 0; i < *returnSize; ++i) {
          (*returnColumnSizes)[i] = k;
      }
      return ans;
  
  }
  ```

  

### 216.组合总和III

- AEAR

  ```
  /**
   * Return an array of arrays of size *returnSize.
   * The sizes of the arrays are returned as *returnColumnSizes array.
   * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
   */
  
  int* path;
  int pathTop;
  int** ans;
  int ansTop;
  
  void backtracking(int targetSum, int k, int sum, int startIndex) {
      if (pathTop == k) {
          if (sum == targetSum) {
              int* temp = (int*)malloc(sizeof(int) * k);
              int j;
              for (j = 0; j < k; ++j) {
                  temp[j] = path[j];
              }
              ans[ansTop++] = temp;
          }
          return;
      }
      for (int i = startIndex; i <= 9; ++i) {
          sum += i;
          path[pathTop++] = i;
          backtracking(targetSum, k, sum, i + 1);
          sum -= i;
          pathTop--;
      }
  }
  
  int** combinationSum3(int k, int n, int* returnSize, int** returnColumnSizes) {
      path = (int*)malloc(sizeof(int) * k);
      ans = (int**)malloc(sizeof(int*) * 20);
      pathTop = ansTop = 0;
  
      backtracking(n, k, 0, 1);
  
      *returnSize = ansTop;
  
      *returnColumnSizes = (int*)malloc(sizeof(int) * ansTop);
      for (int i = 0; i < ansTop; i++) {
          (*returnColumnSizes)[i] = k;
      }
      return ans;
  }
  ```
  
  

### 17.电话号码的字母组合

- csad

  ```
  /**
   * Note: The returned array must be malloced, assume caller calls free().
   */
  char* path;
  int pathTop;
  char** ans;
  int ansTop;
  char* letterMap[10] = {
          "",
          "",
          "abc",
          "def",
          "ghi",
          "jkl",
          "mno",
          "pqrs",
          "tuv",
          "wxyz",
  };
  
  void backtracking(char* digits, int index) {
      if (index == strlen(digits)) {
          char* temp = (char*)malloc(sizeof(char) * strlen(digits) + 1);
          for (int j = 0; j < strlen(digits); j++) {
              temp[j] = path[j];
          }
  
          temp[strlen(digits)] = '\0';
          ans[ansTop++] = temp;
          return;
      }
      int digit = digits[index] - '0';
      char* letters = letterMap[digit];
      for (int i = 0; i < strlen(letters); ++i) {
          path[pathTop++] = letters[i];
          backtracking(digits, index + 1);
          pathTop--;
      }
  }
  
  char** letterCombinations(char* digits, int* returnSize) {
      path = (char*)malloc(sizeof(char) * strlen(digits));
      ans = (char**) malloc(sizeof(char*) * 300);
  
      *returnSize = 0;
      if (strlen(digits) == 0)
          return ans;
  
      pathTop = ansTop = 0;
      backtracking(digits, 0);
  
      *returnSize = ansTop;
      return ans;
  }
  ```

  
### 39. 组合总和

- asd

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
  
  int* length;
  
  void backTracking(int target, int index, int* candidates, int candidatesSize, int sum) {
     if (sum >= target) {
         if (sum == target) {
             int* temp = (int*)malloc(sizeof(int) * pathTop);
             for (int j = 0; j < pathTop; ++j) {
                 temp[j] = path[j];
             }
             ans[ansTop] = temp;
             length[ansTop++] = pathTop;
         }
         return;
     }
     int i;
      for (i = index; i < candidatesSize; i++) {
          path[pathTop++] = candidates[i];
          sum += candidates[i];
          backTracking(target, i, candidates, candidatesSize, sum);
          sum -= candidates[i];
          pathTop--;
      }
  }
  
  int** combinationSum(int* candidates, int candidatesSize, int target, int* returnSize, int** returnColumnSizes) {
      path = (int*)malloc(sizeof(int) * 50);
      ans = (int**)malloc(sizeof(int*) * 200);
      length = (int*)malloc(sizeof(int) * 200);
      ansTop = pathTop = 0;
      backTracking(target, 0, candidates, candidatesSize, 0);
      
      *returnSize = ansTop;
      *returnColumnSizes = (int*)malloc(sizeof(int) * ansTop);
      for (int i = 0; i < ansTop; ++i) {
          (*returnColumnSizes)[i] = length[i];
      }
      
      return ans;
  }
  ```

  

### 40.组合总和II

- dew

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
  int* length;
  
  int cmp(const void* a1, const void* a2) {
      return *((int*)a1) - *((int*)a2);
  }
  
  void backTracking(int* candidates, int candidatesSize, int target, int sum, int startIndex) {
      if(sum >= target) {
          if(sum == target) {
              int* temp = (int*)malloc(sizeof (int) * pathTop);
              for (int j = 0; j < pathTop; ++j) {
                  temp[j] = path[j];
              }
              length[ansTop] = pathTop;
              ans[ansTop++] = temp;
          }
          return;
      }
      for (int i = startIndex; i < candidatesSize; ++i) {
          if(i > startIndex &&  candidates[i] == candidates[i - 1])
              continue;
          path[pathTop++] = candidates[i];
          sum += candidates[i];
          backTracking(candidates, candidatesSize,target, sum, i + 1);
          sum -= candidates[i];
          pathTop--;
      }
  }
  
  int** combinationSum2(int* candidates, int candidatesSize, int target, int* returnSize, int** returnColumnSizes) {
      path = (int*)malloc(sizeof(int) * 50);
      ans = (int**)malloc(sizeof(int*) * 100);
      length = (int*)malloc(sizeof(int) * 100);
      pathTop = ansTop = 0;
  
      qsort(candidates, candidatesSize, sizeof(int), cmp);
  
      backTracking(candidates, candidatesSize, target, 0, 0);
      
      *returnSize = ansTop;
      *returnColumnSizes = (int*)malloc(sizeof(int) * ansTop);
  
      for (int i = 0; i < ansTop; ++i) {
          (*returnColumnSizes)[i] = length[i];
      }
      return ans;
  }
  ```
  
  

### 131.分割回文串

- dsca

  ```
  /**
   * Return an array of arrays of size *returnSize.
   * The sizes of the arrays are returned as *returnColumnSizes array.
   * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
   */
  int** path;
  int pathTop;
  int*** ans;
  int ansTop = 0;
  int* ansSize;
  
  void copy() {
      char** tempPath = (char**)malloc(sizeof(char*) * pathTop);
      for (int i = 0; i < pathTop; ++i) {
          tempPath[i] = path[i];
      }
      ans[ansTop] = tempPath;
      ansSize[ansTop++] = pathTop;
  }
  
  bool isPalindrome(char* str, int startIndex, int endIndex) {
      while (endIndex >= startIndex) {
          if (str[endIndex--] != str[startIndex++])
              return 0;
      }
      return 1;
  }
  
  char * cutString(char* str, int startIndex, int endIndex) {
      char* tempString = (char*)malloc(sizeof(char) * (endIndex - startIndex + 2));
      int i;
      int index = 0;
      for(i = startIndex; i<= endIndex; i++) {
          tempString[index++] = str[i];
      }
      tempString[index] = '\0';
      return tempString;
  }
  
  void backtracking(char* str, int strLen, int startIndex) {
      if(startIndex >= strLen) {
          copy();
          return;
      }
      for (int i = startIndex; i < strLen; ++i) {
          if (isPalindrome(str, startIndex, i)) {
              path[pathTop++] = cutString(str, startIndex, i);
          }
          else {
              continue;
          }
          backtracking(str, strLen, i+1);
          pathTop--;
      }
  }
  char*** partition(char* s, int* returnSize, int** returnColumnSizes) {
      int strLen = strlen(s);
      path = (char**)malloc(sizeof(char*) * strLen);
      ans = (char***)malloc(sizeof(char**) * 40000);
      ansSize = (int*) malloc(sizeof(int) * 40000);
      ansTop = pathTop = 0;
  
      backtracking(s, strLen, 0);
      *returnSize = ansTop;
      *returnColumnSizes = (int*)malloc(sizeof(int) * ansTop);
      for (int i = 0; i < ansTop; ++i) {
          (*returnColumnSizes)[i] = ansSize[i];
      }
      return ans;
  
  }
  ```
  
  
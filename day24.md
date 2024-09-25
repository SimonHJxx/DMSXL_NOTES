### 93.复原IP地址

- sd

  ```
  /**
   * Note: The returned array must be malloced, assume caller calls free().
   */
  
  char** result;
  int resultTop;
  int segments[3];
  
  int isValid(char* s, int start, int end) {
      if (start > end)
          return 0;
      if (s[start] == '0' && start != end)
          return false;
      int num = 0;
      for (int i = start; i <= end; ++i) {
          if (s[i] > '9' || s[i] < '0')
              return false;
          num = num * 10 + (s[i] - '0');
          if (num > 255 )
              return false;
      }
      return true;
  }
  
  void backTracking(char* s, int startIndex, int pointNum) {
      if (pointNum == 3){
          if (isValid(s, startIndex, strlen(s) - 1)) {
              char* tempString = (char*)malloc(sizeof(char) * strlen(s) + 4);
              int j;
              int count = 0;
              int count1 = 0;
              for (j = 0; j < strlen(s); j++){
                  tempString[count++] = s[j];
                  if (count1 < 3 && j == segments[count1]) {
                      tempString[count++] = '.';
                      count1++;
                  }
              }
              tempString[count] = 0;
              result = (char **)realloc(result, sizeof(char *) * (resultTop + 1));
              result[resultTop++] = tempString;
          }
          return;
      }
  
      for (int i = startIndex; i < strlen(s); ++i) {
          if (isValid(s, startIndex, i)) {
              segments[pointNum] = i;
              backTracking(s, i + 1, pointNum + 1);
          }
          else {
              break;
          }
      }
  }
  
  char** restoreIpAddresses(char* s, int* returnSize) {
      result = (char**)malloc(0);
      resultTop = 0;
      backTracking(s, 0, 0);
      *returnSize = resultTop;
      return result;
  }
  ```

  

### 78.子集

- ds

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
  
  void copy() {
      int* tempPath = (int*)malloc(sizeof(int) * pathTop);
      int i;
      for(i = 0; i < pathTop; i++) {
          tempPath[i] = path[i];
      }
      ans = (int**)realloc(ans, sizeof(int*) * (ansTop+1));
      length[ansTop] = pathTop;
      ans[ansTop++] = tempPath;
  }
  
  void backTracking(int* nums, int numsSize, int startIndex) {
      copy();
      if(startIndex >= numsSize) {
          return;
      }
      int j;
      for(j = startIndex; j < numsSize; j++) {
          //将当前下标数字放入path中
          path[pathTop++] = nums[j];
          backTracking(nums, numsSize, j+1);
          pathTop--;
      }
  }
  
  
  int** subsets(int* nums, int numsSize, int* returnSize, int** returnColumnSizes) {
      path = (int*)malloc(sizeof(int) * numsSize);
      ans = (int**)malloc(0);
      length = (int*)malloc(sizeof(int) * 1500);
      ansTop = pathTop = 0;
      backTracking(nums, numsSize, 0);
      *returnSize = ansTop;
      *returnColumnSizes = (int*)malloc(sizeof(int) * ansTop);
      int i;
      for(i = 0; i < ansTop; i++) {
          (*returnColumnSizes)[i] = length[i];
      }
      return ans;
  }
  ```

  

### 90.子集II

- xsa

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
  int* lengths;
  int cmp(const void* a, const void* b) {
      return *((int*)a) - *((int*)b);
  }
  
  void copy() {
      int* tempPath = (int*)malloc(sizeof(int) * pathTop);
      int i;
      for(i = 0; i < pathTop; i++) {
          tempPath[i] = path[i];
      }
      ans = (int**)realloc(ans, sizeof(int*) * (ansTop + 1));
      lengths[ansTop] = pathTop;
      ans[ansTop++] = tempPath;
  }
  
  void backTracking(int* nums, int numsSize, int startIndex) {
      copy();
      if(startIndex >= numsSize)
          return ;
  
      int i;
      for(i = startIndex; i < numsSize; i++) {
          //对同一树层使用过的元素进行跳过
          if(i > startIndex && nums[i] ==  nums[i-1] )
              continue;
          path[pathTop++] = nums[i];
          backTracking(nums, numsSize, i + 1);
          pathTop--;
      }
  }
  
  int** subsetsWithDup(int* nums, int numsSize, int* returnSize, int** returnColumnSizes){
      path = (int*)malloc(sizeof(int) * numsSize);
      ans = (int**)malloc(0);
      lengths = (int*)malloc(sizeof(int) * 1500);
      pathTop = ansTop = 0;
  
      qsort(nums, numsSize, sizeof(int), cmp);
      backTracking(nums, numsSize, 0);
  
      *returnSize = ansTop;
      *returnColumnSizes = (int*)malloc(sizeof(int) * ansTop);
      int i;
      for(i = 0; i < ansTop; i++) {
          (*returnColumnSizes)[i] = lengths[i];
      }
      return ans;
  }
  
  
  
  
  
  
  int* path;
  int pathTop;
  int** ans;
  int ansTop;
  int* length;
  
  void copy() {
      int* tempPath = (int*)malloc(sizeof(int) * pathTop);
      memcpy(tempPath, path, pathTop * sizeof(int));
      length[ansTop] = pathTop;
      ans[ansTop++] = tempPath;
  }
  
  
  int find(int* uset, int usetSize, int key) {
      int i;
      for(i = 0; i < usetSize; i++) {
          if(uset[i] == key)
              return 1;
      }
      return 0;
  }
  
  void backTracking(int* nums, int numsSize, int startIndex) {
  
      if(pathTop > 1) {
          copy();
      }
      int* uset = (int*)malloc(sizeof(int) * numsSize);
      int usetTop = 0;
      int i;
      for(i = startIndex; i < numsSize; i++) {
  
          if((pathTop > 0 && nums[i] < path[pathTop - 1]) || find(uset, usetTop, nums[i]))
              continue;
  
          uset[usetTop++] = nums[i];
  
          path[pathTop++] = nums[i];
          backTracking(nums, numsSize, i + 1);
  
          pathTop--;
      }
  }
  
  int** findSubsequences(int* nums, int numsSize, int* returnSize, int** returnColumnSizes){
  
      path = (int*)malloc(sizeof(int) * numsSize);
      ans = (int**)malloc(sizeof(int*) * 33000);
      length = (int*)malloc(sizeof(int*) * 33000);
      pathTop = ansTop = 0;
  
      backTracking(nums, numsSize, 0);
      
      *returnSize = ansTop;
      *returnColumnSizes = (int*)malloc(sizeof(int) * ansTop);
      int i;
      for(i = 0; i < ansTop; i++) {
          (*returnColumnSizes)[i] = length[i];
      }
      return ans;
  }
  ```

  

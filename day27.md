### 理论基础

- **贪心的本质是选择每一阶段的局部最优，从而达到全局最优**
- 

### 455.分发饼干

- s

  ```
  
  int cmp(int* a, int* b) {
      return *a - *b;
  }
  
  int findContentChildren(int* g, int gSize, int* s, int sSize) {
      if(sSize == 0)
          return 0;
      qsort(g, gSize, sizeof(int), cmp);
      qsort(s, sSize, sizeof(int), cmp);
      int numFedChildren = 0;
      for (int i = 0; i < sSize; ++i) {
          if(numFedChildren < gSize && g[numFedChildren] <= s[i])
              numFedChildren++;
      }
      return numFedChildren;
  }
  
  
  
  int cmp(int* a, int* b) {
      return *a - *b;
  }
  
  int findContentChildren(int* g, int gSize, int* s, int sSize) {
      if(sSize == 0)
          return 0;
      qsort(g, gSize, sizeof(int), cmp);
      qsort(s, sSize, sizeof(int), cmp);
      int count = 0;
      int start = sSize - 1;
      for (int i = gSize - 1; i >= 0; i--) {
          if(start >= 0 && s[start] >= g[i]) {
              start--;
              count++;
          }
      }
      return count;
  }
  ```

  

### 376. 摆动序列

- s

  ```
  int wiggleMaxLength(int* nums, int numsSize){
      if(numsSize <= 1)
          return numsSize;
      int length = 1;
      int preDiff, curDiff;
      preDiff = curDiff = 0;
      for (int i = 0; i < numsSize - 1; ++i) {
           curDiff = nums[i + 1] - nums[i];
           if((curDiff > 0 && preDiff <= 0) || (curDiff < 0 && preDiff >= 0)) {
               preDiff = curDiff;
               length++;
           }
      }
      return length;
  }
  ```

  

### 53. 最大子序和

- qdw

  ```
  int maxSubArray(int* nums, int numsSize) {
      int maxVAL = INT_MIN;
      int subArrSum = 0;
  
      for (int i = 0; i < numsSize; ++i) {
          subArrSum += nums[i];
          maxVAL = subArrSum > maxVAL ? subArrSum : maxVAL;
          subArrSum = subArrSum < 0 ? 0 : subArrSum;
      }
      return maxVAL;
  }
  ```

  
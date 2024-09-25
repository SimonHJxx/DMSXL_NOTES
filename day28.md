### 122.买卖股票的最佳时机II

- wq

  ```
  int maxProfit(int* prices, int pricesSize) {
      int result = 0;
      for (int i = 0; i < pricesSize - 1; ++i) {
          if(prices[i + 1] > prices[i])
              result += prices[i + 1] - prices[i];
      }
      return result;
  }
  ```
  
  

### 55. 跳跃游戏

- xca

  ```
  
  #define max(a, b) (((a) > (b)) ? (a) : (b))
  
  bool canJump(int* nums, int numsSize) {
      int cover = 0;
      for (int i = 0; i <= cover; ++i) {
          cover = max(i + nums[i], cover);
          if (cover >= numsSize - 1)
              return true;
      }
      return false;
  }
  ```
  
  

### 45.跳跃游戏II

- dq

  ```
  ```

  

### 1005.K次取反后最大化的数组和

- we

  ```
  
  #define abs(a) (((a) > 0) ? (a) : (-(a)))
  
  int sum(int* nums, int numsSize) {
      int sum = 0;
      for (int i = 0; i < numsSize; i++) {
          sum += nums[i];
      }
      return sum;
  }
  
  int cmp(const void* v1, const void* v2) {
      return abs(*(int*)v2) - abs(*(int*)v1);
  }
  
  int largestSumAfterKNegations(int* nums, int numsSize, int k) {
      qsort(nums, numsSize, sizeof(int), cmp);
      for (int i = 0; i < numsSize; ++i) {
          if(nums[i] < 0 && k > 0) {
              nums[i] = -nums[i];
              k--;
          }
      }
      if(k % 2) {
          nums[numsSize - 1] = -nums[numsSize - 1];
      }
      return sum(nums, numsSize);
  }
  ```
  
  
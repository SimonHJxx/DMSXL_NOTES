### 理论基础

1. 确定dp数组（dp table）以及下标的含义
2. 确定递推公式
3. dp数组如何初始化
4. 确定遍历顺序
5. 举例推导dp数组

### 509. 斐波那契数

- d

  ```
  
  
  int fib(int n){
      if(n <= 1)
          return n;
      int *dp = (int*)malloc(sizeof(int) * (n + 1));
      dp[0] = 0;
      dp[1] = 1;
  
      for (int i = 2; i <= n; ++i) {
          dp[i] = dp[i - 1] + dp[i - 2];
      }
      return dp[n];
  }
  ```
  
  

### 70. 爬楼梯

- cds

  ```
  int climbStairs(int n) {
      if(n <= 2)
          return n;
      int* dp = (int*)malloc(sizeof(int) * (n + 1));
      dp[0] = 0;
      dp[1] = 1;
      dp[2] = 2;
      for(int i = 3; i <= n; i++) {
          dp[i] = dp[i - 1] + dp[i - 2];
      }
      return dp[n];
  }
  ```
  
  

### 746. 使用最小花费爬楼梯

- cw

  ```
  int minCostClimbingStairs(int* cost, int costSize) {
      int dp[costSize + 1];
      dp[0] = dp[1] = 0;
      for (int i = 2; i <= costSize; ++i) {
          dp[i] = fmin(dp[i - 1] + cost[i - 1], dp[i - 2] + cost[i - 2]);
      }
      return dp[costSize];
  }
  ```
  
  
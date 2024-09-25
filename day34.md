### 62.不同路径

- xds

  ```
  int** ininDP(int m, int n) {
      int** dp = (int**)malloc(sizeof(int*) * m);
      int i, j;
      for (i = 0; i < m, ++i)
      {
          dp[i] = (int*)malloc(sizeof(int) * n);
      }
      for (i = 0; i < m; ++) {
          dp[i][0] = 1;
      }
      for (j = 0; j < n; ++) {
          dp[0][j] = 1;
      }
      return dp;
  }
  
  int uniquePaths(int m, int n) {
      int** dp = initDP(m, n);
      int i, j;
      for (i = 1; i < m; ++i) {
          for (j = 1; j < n; ++j) {
              dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
          }
      }
      int result = dp[m - 1][n - 1];
      free(dp);
      return result;
  }
  ```

  

### 63. 不同路径 II

- sw

  ```
  
  int** initDP(int m, int n, int** obstacleGrid) {
      int** dp = (int**)malloc(sizeof(int*) * m);
      int i, j;
      for (i = 0; i < m; ++i)
      {
          dp[i] = (int*)malloc(sizeof(int) * n);
      }
      for (i = 0; i < m; ++i) {
          dp[i][0] = 0;
      }
      for (j = 0; j < n; ++j) {
          dp[0][j] = 0;
      }
  
      for (i = 0; i < m; ++i) {
          if (obstacleGrid[i][0])
              break;
          dp[i][0] = 1;
      }
  
      for (j = 0; j < n; ++j) {
          if (obstacleGrid[0][j])
              break;
          dp[0][j] = 1;
      }
      return dp;
  }
  
  int uniquePathsWithObstacles(int** obstacleGrid, int obstacleGridSize, int* obstacleGridColSize) {
      int m = obstacleGridSize, n = *obstacleGridColSize;
      int** dp = initDP(m, n, obstacleGrid);
      for (int i = 1; i < m; ++i) {
          for (int j = 1; j < n; ++j) {
              if (obstacleGrid[i][j])
                  dp[i][j] = 0;
              else
                  dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
          }
      }
      return dp[m - 1][n - 1];
  }
  ```
  
  

### 343. 整数拆分 （可跳过）

### 96. 不同的二叉搜索树 （可跳过）


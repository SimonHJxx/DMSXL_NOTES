### 452. 用最少数量的箭引爆气球

- dw

  ```
  
  int cmp(const void* a, const void* b) {
      return ((*((int**)a))[0] > (*((int**)b))[0]);
  }
  
  int findMinArrowShots(int** points, int pointsSize, int* pointsColSize) {
      qsort(points, pointsSize, sizeof(points[0]), cmp);
      int arrowNum = 1;
      for (int i = 1; i < pointsSize; ++i) {
          if(points[i][0] > points[i - 1][1])
              arrowNum ++;
          else
              points[i][1] = points[i][1] > points[i - 1][1] ? points[i - 1][1] : points[i][1];
      }
      return arrowNum;
  }
  ```

  

### 435. 无重叠区间

- wq

  ```
  
  int cmp(const void* var1, const void* var2) {
      return (*(int**)var1)[1] - (*(int**)var2)[1];
  }
  
  int eraseOverlapIntervals(int** intervals, int intervalsSize, int* intervalsColSize) {
      if (intervalsSize == 0) {
          return 0;
      }
      qsort(intervals, intervalsSize, sizeof(int*), cmp);
      int count = 1;
      int end = intervals[0][1];
      for (int i = 1; i < intervalsSize; i++) {
          if (intervals[i][0] >= end) {
              count++;
              end = intervals[i][1];
          }
      }
      return intervalsSize - count;
  }
  ```

  

### 763.划分字母区间

- dew

  ```
  /**
   * Note: The returned array must be malloced, assume caller calls free().
   */
  
  #define max(a, b) ((a) > (b) ? (a) : (b))
  
  int* partitionLabels(char* s, int* returnSize) {
      int last[26] = {0};
      int len = strlen(s);
      for (int i = 0; i < len; ++i) {
          last[s[i] - 'a'] = i;
      }
      int left = 0, right = 0;
      int* partition = malloc(sizeof(int) * len);
      *returnSize = 0;
      for (int i = 0; i < len; ++i) {
          right = max(right, last[s[i] - 'a']);
          if (i == right) {
              partition[(*returnSize)++] = right - left + 1;
              left = right + 1;
          }
      }
      return partition;
  }
  ```

  
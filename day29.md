### 134. 加油站

- sa

  ```
  int canCompleteCircuit(int* gas, int gasSize, int* cost, int costSize) {
  int curSum = 0;
  int totalSum = 0;
  int start = 0;
      for (int i = 0; i < gasSize; ++i) {
          int diff = gas[i] - cost[i];
          curSum += diff;
          totalSum += diff;
          if (curSum < 0) {
              curSum = 0;
              start = i + 1;
          }
      }
      if (totalSum < 0)
          return -1;
      return start;
  }
  ```
  
  

### 135. 分发糖果

- f

  ```
  #define max(a, b) (((a) > (b)) ? (a) : (b))
  
  int* initCandyArr(int size) {
      int* candyArr = (int*)malloc(sizeof(int) * size);
      for (int i = 0; i < size; ++i) {
          candyArr[i] = 1;
      }
      return candyArr;
  }
  
  int candy(int* ratings, int ratingsSize) {
      int* candyArr = initCandyArr(ratingsSize);
      for (int i = 1; i < ratingsSize; ++i) {
          if (ratings[i] > ratings[i - 1])
              candyArr[i] = candyArr[i - 1] + 1;
      }
  
      for (int i = ratingsSize - 2; i >= 0; --i) {
          if(ratings[i] > ratings[i + 1])
              candyArr[i] = max(candyArr[i], candyArr[i + 1] + 1);
      }
      int result = 0;
      for (int i = 0; i < ratingsSize; ++i) {
          result += candyArr[i];
      }
      return result;
  }
  ```
  
  

### 860.柠檬水找零

- dsrfe

  ```
  bool lemonadeChange(int* bills, int billsSize) {
      int fiveCount = 0;
      int tenCount = 0;
      for (int i = 0; i < billsSize; ++i) {
          switch (bills[i]) {
              case 5:
                  fiveCount++;
                  break;
              case 10:
                  if (fiveCount == 0) {
                      return false;
                  }
                  fiveCount--;
                  tenCount++;
                  break;
              case 20:
                  if (fiveCount > 0 && tenCount > 0){
                      fiveCount--;
                      tenCount--;
                  }
                  else if (fiveCount >= 3) {
                      fiveCount -= 3;
                  } 
                  else
                      return false;
                  break;
          }
      }
      return true;
  }
  ```
  
  

### 406.根据身高重建队列

- fvd

  ```
  ```

  
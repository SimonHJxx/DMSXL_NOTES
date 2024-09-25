### 56. 合并区间

- qw

  ```
  ```

  

### 738.单调递增的数字

- dw

  ```
  int monotoneIncreasingDigits(int n) {
      char str[11];
      sprintf(str, "%d", n);
      int len = strlen(str);
      int flag = strlen(str);
      for (int i = len - 1; i > 0 ; --i) {
          if (str[i] < str[i - 1]) {
              str[i - 1]--;
              flag = i;
          }
      }
      for (int i = flag; i < len; ++i) {
          str[i] = '9';
      }
      return atoi(str);
  }
  ```

  

### 968.监控二叉树 （可跳过）
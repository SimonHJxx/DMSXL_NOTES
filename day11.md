### 150. 逆波兰表达式求值


- 分组+哈希表

  ```
  bool isNumber(char* token){
      return strlen(token) > 1 || token[0] >= '0' && token[0] <= '9';
  }
  
  int evalRPN(char** tokens, int tokensSize) {
      int n = tokensSize;
      int stk[n], top = 0;
      for (int i = 0; i < n; ++i) {
          char* token = tokens[i];
          if(isNumber(token)){
              //int atoi(const char *str)把参数str所指向的字符串转换为一个整数（类型为int型）
              stk[top++] = atoi(token);
          }
          else{
              int num2 = stk[--top];
              int num1 = stk[--top];
              switch (token[0]){
                  case '+':
                      stk[top++] = num1 + num2;
                      break;
                  case '-':
                      stk[top++] = num1 - num2;
                      break;
                  case '*':
                      stk[top++] = num1 * num2;
                      break;
                  case '/':
                      stk[top++] = num1 / num2;
                      break;
              }
          }
      }
      return stk[--top];
  }
  ```
  
  

### 239. 滑动窗口最大值

- 

  ```
  
  ```

  

### 347.前 K 个高频元素

- 

  ```
  
  ```

### 344.反转字符串

- 头尾互相交换即可

  ```
  void reverseString(char* s, int sSize) {
      int left = 0;
      int right = sSize - 1;
  
      while(left < right){
          char tmp = s[left];
          s[left] = s[right];
          s[right] = tmp;
          left++;
          right--;
      }
  
  }
  ```
  
  

### 541. 反转字符串II

- 

  ```
  char* reverseStr(char* s, int k) {
      /*
       * size_t strlen(const char *str),
       * str-要计算长度的字符串
       */
      int len = strlen(s);
      for (int i = 0; i < len; i += (2 * k)) {
          k =  i + k > len ? len - i : k;
          int left = i;
          int right = i + k - 1;
          while(left < right){
              char tmp = s[left];
              s[left] = s[right];
              s[right] = tmp;
              left++;
              right--;
          }
      }
      return s;
  
  }
  ```
  
  

### 卡码网：54.替换数字

- 

  ```
  #include <stdio.h>
  #include <string.h>
  
  int main()
  {
      int length = 0;
      int num_count = 0;
      char input_str[10000];
  
      printf("iuput your string: ");
      scanf("%s", input_str);
      length = strlen(input_str);
      printf("your string length is: %d \n", length);
  
      for (int i = 0; i < length; ++i) {
          if(input_str[i] >= '0' && input_str[i] <= '9'){
              num_count++;
          }
      }
  
      printf("num_count:%d \n", num_count);
      int index = length + num_count * 5 + 1;
      char output_str[index];
  
      for (int j = 0; j < index - 1; ++j) {
          output_str[j] = input_str[j];
      }
      printf("index: %d \n", index);
      int k = length - 1;
      index = index - 2;
      while ( k >= 0){
          if(output_str[k] >= '0' && output_str[k] <= '9'){
              output_str[index--] = 'r';
              output_str[index--] = 'e';
              output_str[index--] = 'b';
              output_str[index--] = 'm';
              output_str[index--] = 'u';
              output_str[index--] = 'n';
          }
          else{
              output_str[index--] = output_str[k];
          }
          k--;
      }
  
      printf("output_str: %s \n", output_str);
  
      return 0;
  
  }
  
  
  ```
  
  

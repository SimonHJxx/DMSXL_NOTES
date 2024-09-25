### 151.翻转字符串里的单词


- 

  ```
  // 翻转指定范围的字符串
  void reverse(char* s, int start, int end)
  {
      for (int i = start, j = end; i < j; i++, j--) {
          int tmp = s[i];
          s[i] = s[j];
          s[j] = tmp;
      }
  }
  
  // 删除多余的空字符并重新生成字符串
  void removeExtraSpace(char* s)
  {
      // 旧字符串的首尾索引
      int start = 0;
      int end = strlen(s) - 1;
      // 删除首部空字符
      while(s[start] == ' ') start++;
      // 删除尾部空字符
      while(s[end] == ' ') end--;
      // 新字符串索引
      int slow = 0;
      for (int i = start; i <= end; ++i) {
          // 删除字符串中的多余空字符
          if(s[i] == ' ' && s[i+1] == ' ') continue;
          // 新字符串
          s[slow++] = s[i];
      }
      // 添加字符串标识
      s[slow] = '\0';
  }
  
  char* reverseWords(char* s) {
      removeExtraSpace(s);
      reverse(s, 0, strlen(s) - 1);
      // 翻转每个单词
      int slow = 0;
      for (int i = 0; i <= strlen(s); ++i) {
          if(s[i] == ' ' || s[i] == '\0'){
              reverse(s, slow, i - 1);
              slow = i + 1;
          }
      }
      return s;
  }
  ```
  
  

### 卡码网：55.右旋转字符串

- 

  ```
  #include <stdio.h>
  #include <string.h>
  
  void reverse(char* s, int left, int right)
  {
      while (left <= right){
          char c = s[left];
          s[left] = s[right];
          s[right] = c;
          left++;
          right--;
      }
  }
  
  void rightRotate(char* s, int k)
  {
      int len = strlen(s);
      reverse(s, 0, len - k - 1);
      reverse(s, len - k, len - 1);
      reverse(s, 0, len - 1);
  }
  
  int main()
  {
      int k;
      scanf("%d", &k);
      char s[10000];
      scanf("%s", s);
      rightRotate(s, k);
      printf("%s\n", s);
  
      return 0;
  }
  ```
  
  

### 28. 实现 strStr()

- 

  ```
  
  
  int strStr(char* haystack, char* needle) {
      int n, m;
      n = strlen(haystack);
      m = strlen(needle);
  
      if (m == 0) {
          return 0;
      }
  
      int next[m];
      next[0] = 0;
      for (int i = 1, j = 0; i < m; ++i) {
          while (j > 0 && (needle[i] != needle[j])){
              j = next[j - 1];
          }
          if (needle[i] == needle[j]){
              j++;
          }
          next[i] = j;
      }
      for (int i = 0, j = 0; i < n; ++i) {
          while (j > 0 && (haystack[i] != needle[j])){
              j = next[j - 1];
          }
          if (haystack[i] == needle[j]){
              j++;
          }
          if (j == m){
              return i - m + 1;
          }
      }
      return -1;
  
  }
  ```

### 459.重复的子字符串

- 

  ```
  ```

  

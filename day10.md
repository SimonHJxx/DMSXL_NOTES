### 理论基础


- 


### 232.用栈实现队列

- 两个栈模拟一个队列

  ```
  
  
  // 定义两个栈，入栈与出栈，定义栈顶指针
  typedef struct {
      int stackInTop, stackOutTop;
      int stackIn[100], stackOut[100];
  
  } MyQueue;
  
  // 开辟队列空间，并初始化栈顶指针为0
  MyQueue* myQueueCreate() {
      MyQueue* queue = (MyQueue*)malloc(sizeof(MyQueue));
      queue -> stackInTop = 0;
      queue -> stackOutTop = 0;
      return queue;
  }
  
  
  void myQueuePush(MyQueue* obj, int x) {
      obj -> stackIn[obj -> stackInTop] = x;
      (obj -> stackInTop)++;
  }
  
  
  int myQueuePop(MyQueue* obj) {
      int stackInTop = obj -> stackInTop;
      int stackOutTop = obj -> stackOutTop;
  
      if(stackOutTop == 0){
          while (stackInTop > 0){
              obj -> stackOut[stackOutTop++] = obj -> stackIn[--stackInTop];
          }
      }
      int top = obj -> stackOut[--stackOutTop];
      while (stackOutTop > 0){
          obj -> stackIn[stackInTop++] = obj -> stackOut[--stackOutTop];
      }
      obj -> stackInTop = stackInTop;
      obj -> stackOutTop = stackOutTop;
      
      return top;
  }
  
  int myQueuePeek(MyQueue* obj) {
      return obj -> stackIn[0];
  }
  
  bool myQueueEmpty(MyQueue* obj) {
      return obj -> stackInTop == 0 && obj -> stackOutTop == 0;
  }
  
  void myQueueFree(MyQueue* obj) {
      obj -> stackInTop = 0;
      obj -> stackOutTop = 0;
  }
  
  /**
   * Your MyQueue struct will be instantiated and called as such:
   * MyQueue* obj = myQueueCreate();
   * myQueuePush(obj, x);
  
   * int param_2 = myQueuePop(obj);
  
   * int param_3 = myQueuePeek(obj);
  
   * bool param_4 = myQueueEmpty(obj);
  
   * myQueueFree(obj);
  */
  
  ```
  
  

### 225. 用队列实现栈

- 

  ```
  
  typedef struct tagListNode{
      struct tagListNode* next;
      int val;
  } ListNode;
  
  typedef struct {
      ListNode *top;
  
  } MyStack;
  
  
  MyStack* myStackCreate() {
      MyStack *stk = (MyStack*)calloc(1, sizeof(MyStack));
      return stk;
  }
  
  void myStackPush(MyStack* obj, int x) {
      ListNode *node = (ListNode*)malloc(sizeof(ListNode));
      node -> val = x;
      node -> next = obj -> top;
      obj -> top = node;
  }
  
  int myStackPop(MyStack* obj) {
      ListNode *node = obj -> top;
      int val = node -> val;
      obj -> top = node -> next;
      free(node);
      return val;
  }
  
  int myStackTop(MyStack* obj) {
      return obj -> top -> val;
  }
  
  bool myStackEmpty(MyStack* obj) {
      return (obj -> top == NULL);
  }
  
  void myStackFree(MyStack* obj) {
      while (obj -> top != NULL){
          ListNode *node = obj -> top;
          obj -> top = node -> next;
          free(node);
      }
      free(obj);
  }
  
  /**
   * Your MyStack struct will be instantiated and called as such:
   * MyStack* obj = myStackCreate();
   * myStackPush(obj, x);
  
   * int param_2 = myStackPop(obj);
  
   * int param_3 = myStackTop(obj);
  
   * bool param_4 = myStackEmpty(obj);
  
   * myStackFree(obj);
  */
  ```

### 20. 有效的括号

- 

  ```
  int notMatch(char par,  char* stack, int stackTop){
      switch (par) {
          case ']':
              return stack[stackTop - 1] == '[';
          case ')':
              return stack[stackTop - 1] == '(';
          case '}':
              return stack[stackTop - 1] == '{';
      }
      return 0;
  }
  
  bool isValid(char* s) {
      int length = strlen(s);
      char stack[5000];
      int stackTop = 0;
  
      int i;
      for (int i = 0; i < length; ++i) {
          char tempChar = s[i];
          if(tempChar == '[' ||tempChar == '(' ||tempChar == '{'){
              stack[stackTop++] = tempChar;
          }
          else if(stackTop == 0 || !(notMatch(tempChar, stack, stackTop))){
              return 0;
          }
          else{
              --stackTop;
          }
      }
      return !stackTop;
  }
  ```

  

### 1047. 删除字符串中的所有相邻重复项

- 

  ```
  char* removeDuplicates(char* s) {
      int strlength = strlen(s);
      char* stack = (char*)malloc(sizeof(char) * (strlength + 1));
      int stacktop = 0;
  
      int i = 0;
      while (i < strlength) {
          char letter = s[i];
          i++;
          if(stacktop > 0 && letter == stack[stacktop - 1]){
              stacktop--;
          }
          else
              stack[stacktop++] = letter;
      }
      stack[stacktop] = '\0';
  
      return stack;
  }
  ```

  
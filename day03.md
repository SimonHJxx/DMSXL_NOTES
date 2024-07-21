### **链表理论基础**

- 什么是链表，链表是一种通过指针串联在一起的线性结构，每一个节点由两部分组成，一个是数据域一个是指针域（存放指向下一个节点的指针），最后一个节点的指针域指向null（空指针的意思）。

- 链表的入口节点称为链表的头结点也就是head。

- 单链表：单链表中的指针域只能指向节点的下一个节点。

- 双链表：每一个节点有两个指针域，一个指向下一个节点，一个指向上一个节点。双链表既可以向前查询也可以向后查询。

- 循环链表：顾名思义，就是链表首尾相连。循环链表可以用来解决约瑟夫环问题。

- 存储方式：数组是在内存中是连续分布的，但是链表在内存中可不是连续分布的。链表是通过指针域的指针链接在内存中各个节点。所以链表中的节点在内存中不是连续分布的 ，而是散乱分布在内存中的某地址上，分配机制取决于操作系统的内存管理。

- 链表的定义

  ```
  struct ListNode{
  	int val;
  	struct ListNodeT *next;
  };
  ```

  

### **203.移除链表元素**

- 不要忘了还要从内存中删除这两个移除的节点

- **用原来的链表操作**

  ```
  /**
   * Definition for singly-linked list.
   * struct ListNode {
   *     int val;
   *     struct ListNode *next;
   * };
   */
  struct ListNode* removeElements(struct ListNode* head, int val) {
      struct ListNode *temp;
      while (head && (head->val == val)) //一直循环到头结点数值不同或者头指针指向NULL
      {
          temp = head;
          head = head->next;
          free(temp);
      }
      struct ListNode *cur = head;
      while (cur && (cur->next != NULL)) //判断头结点存在并且头结点后续有其他结点
      {
          temp = cur->next;
          if(cur->next->val == val)
          {
              cur->next = cur->next->next;
              free(temp);
          }
          else
          {
              cur = cur->next;
          }
      }
      return head;
  }
  
  ```

  

- **设置一个虚拟头结点**

  ```
  /**
   * Definition for singly-linked list.
   * struct ListNode {
   *     int val;
   *     struct ListNode *next;
   * };
   */
  struct ListNode* removeElements(struct ListNode* head, int val) {
      struct ListNode *virtual; //定义指向虚拟头结点的指针
      virtual = (struct ListNode*) malloc(sizeof(struct ListNode)); //分配头结点内存空间并将virtual指向这个头结点
      virtual->next = head; //头结点的尾指针指向第一个结点
      struct ListNode *cur = virtual;
      while (cur->next != NULL) //循环条件判断
      {
          if (cur->next->val == val){
              struct ListNode *tmp = cur->next; //预先存储稍后要释放的内存空间
              cur->next = cur->next->next;
              free(tmp);
          }
          else{
              cur = cur->next; //cur指针后移
          }
      }
      head = virtual->next; //还原头指针
      free (virtual); //释放头结点内存空间
      return head;
  }
  
  ```

  


### **707.设计链表**

```
typedef struct {
    int val;
    struct ListNode* next;
} MyLinkedList;

//创建虚拟头结点
MyLinkedList* myLinkedListCreate() {
    MyLinkedList* head = (MyLinkedList*)malloc(sizeof (MyLinkedList));
    head->next = NULL;
    return head;
}

int myLinkedListGet(MyLinkedList* obj, int index) {
    MyLinkedList* cur = obj->next;
    for (int i = 0; cur != NULL; ++i) {
        if(i == index){
            return cur->val;
        }
        else{
            cur = cur->next;
        }
    }
    return -1;
}

void myLinkedListAddAtHead(MyLinkedList* obj, int val) {
    MyLinkedList* newhead = (MyLinkedList*) malloc(sizeof (MyLinkedList));
    newhead->val = val;
    newhead->next = obj->next;
    obj->next = newhead;
}

void myLinkedListAddAtTail(MyLinkedList* obj, int val) {

    MyLinkedList* cur = obj;
    while (cur->next != NULL){
        cur = cur->next;
    }
    MyLinkedList* newtail = (MyLinkedList*) malloc(sizeof (MyLinkedList));
    newtail->next = NULL;
    newtail->val = val;
    cur->next = newtail;
}

void myLinkedListAddAtIndex(MyLinkedList* obj, int index, int val) {
    if(index == 0){
        myLinkedListAddAtHead(obj,val);
        return;
    }
    MyLinkedList* cur = obj->next;
    for (int i = 1; cur != NULL; ++i) {
        if(i == index){
            MyLinkedList* newnode = (MyLinkedList*) malloc(sizeof (MyLinkedList));
            newnode->val = val;
            newnode->next = cur->next;
            cur->next = newnode;
            return;
        }
        cur = cur->next;
    }
}

void myLinkedListDeleteAtIndex(MyLinkedList* obj, int index) {
    if(index == 0){
        MyLinkedList* temp = obj->next;
        if(temp != NULL){
            obj->next = temp->next;
            free(temp);
        }
        return;
    }
    MyLinkedList* cur = obj->next;
    for (int i = 1; cur != NULL; ++i) {
        if(i == index){
            MyLinkedList* temp= cur->next;
            if(temp != NULL){
                cur->next = temp->next;
                free(temp);
            }
        }
        cur = cur->next;
    }
}

void myLinkedListFree(MyLinkedList* obj) {
    while (obj != NULL){
        MyLinkedList * temp = obj;
        obj = obj->next;
        free(temp);
    }
}

/**
 * Your MyLinkedList struct will be instantiated and called as such:
 * MyLinkedList* obj = myLinkedListCreate();
 * int param_1 = myLinkedListGet(obj, index);

 * myLinkedListAddAtHead(obj, val);

 * myLinkedListAddAtTail(obj, val);

 * myLinkedListAddAtIndex(obj, index, val);

 * myLinkedListDeleteAtIndex(obj, index);

 * myLinkedListFree(obj);
*/
```



###  **206.反转链表**

-  双指针法

  ```
  /**
   * Definition for singly-linked list.
   * struct ListNode {
   *     int val;
   *     struct ListNode *next;
   * };
   */
  struct ListNode* reverseList(struct ListNode* head) {
      struct ListNode* pre = NULL;
      struct ListNode* temp;
      while(head){
          temp = head->next;
          head->next = pre;
          pre = head;
          head = temp;
      }
      return pre;
  }
  ```

  

- 递归法

  ```
  /**
   * Definition for singly-linked list.
   * struct ListNode {
   *     int val;
   *     struct ListNode *next;
   * };
   */
  struct ListNode* reverse(struct ListNode* pre, struct ListNode* cur){
      if(cur == NULL) //递归结束条件
      {
          return pre;
      }
      struct ListNode* temp = cur->next; //打标签
      cur->next = pre; //改变当前结点指向
      return reverse(cur,temp); //整体后移进入递归
  }
  
  struct ListNode* reverseList(struct ListNode* head) {
      return reverse(NULL,head);
  }
  ```

  


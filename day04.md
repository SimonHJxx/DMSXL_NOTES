### 24. 两两交换链表中的节点

- 递归版本

  ```
  /**
   * Definition for singly-linked list.
   * struct ListNode {
   *     int val;
   *     struct ListNode *next;
   * };
   */
  struct ListNode* swapPairs(struct ListNode* head) {
      //递归的结束条件
      if (!head || !head->next) return head;
      /*每两个结点是一次递归窗口
       * 保证每次进入递归时，创建新的指针指向窗口的第二个结点
       * 在递归函数内，改变窗口内结点的指向
       * 每次递归结束时，返回创建的新指针
       */
      struct ListNode* newhead = head->next;
      head->next = swapPairs(newhead->next);
      newhead->next = head;
      return newhead;
  
  }
  ```

  

- 迭代版本

  ```
  #include <malloc.h>
  
  /**
   * Definition for singly-linked list.
   * struct ListNode {
   *     int val;
   *     struct ListNode *next;
   * };
   */
  struct ListNode* swapPairs(struct ListNode* head) {
      struct ListNode* virtual = (struct ListNode*) malloc(sizeof (struct ListNode));
      virtual->next = head;
      struct ListNode* left = virtual;
      struct ListNode* right = virtual->next;
      while (left && right && right->next)
      {
      	//前三步修改内部指向
          left->next = right->next;
          right->next = left->next->next;
          left->next->next = right;
          //后两步修改下次循环初始条件
          left = right;
          right = right->next;
      }
      return virtual->next;
  }
  
  ```

  

### 19.删除链表的倒数第N个节点

- 设置快慢指针，初始都指向虚拟结点

- 快指针先走n+1步

- 随后快慢指针同时后移直到快指针指向NULL

- 删除慢指针指向的下一个结点

  ```
  /**
   * Definition for singly-linked list.
   * struct ListNode {
   *     int val;
   *     struct ListNode *next;
   * };
   */
  struct ListNode* removeNthFromEnd(struct ListNode* head, int n) {
      struct ListNode* virtual = (struct ListNode*)malloc(sizeof (struct ListNode));
      virtual->next = head;
      struct ListNode* slow = virtual;
      struct ListNode* fast = virtual;
      for (int i = 0; i < n + 1; ++i) {
          fast = fast->next;
      }
      while (fast){
          fast = fast->next;
          slow = slow->next;
      }
      slow->next = slow->next->next;
      head = virtual->next;
      free(virtual);
      return head;
  }
  ```

  


### 面试题 02.07. 链表相交

- 假设节点元素数值相等，则节点指针相等

  ```
  /**
   * Definition for singly-linked list.
   * struct ListNode {
   *     int val;
   *     struct ListNode *next;
   * };
   */
  struct ListNode *getIntersectionNode(struct ListNode *headA, struct ListNode *headB) {
      struct ListNode* aln = headA;
      struct ListNode* bln = headB;
      int lenA = 0, lenB = 0, gap = 0;
  
      while (aln){
          lenA ++;
          aln = aln->next;
      }
      while (bln){
          lenB ++;
          bln = bln->next;
      }
  
      aln = headA;
      bln = headB;
      if (lenA > lenB){
          gap = lenA - lenB;
          while (gap){
              aln = aln->next;
              gap --;
          }
          while (aln){
              if (aln == bln) return aln;
              aln = aln->next;
              bln = bln->next;
          }
      }
      else {
          gap = lenB - lenA;
          while (gap){
              bln = bln->next;
              gap --;
          }
          while (bln){
              if (aln == bln) return bln;
              aln = aln->next;
              bln = bln->next;
          }
      }
      return NULL;
  }
  ```

  

###  142.环形链表II

- 快慢指针法，分别定义 fast 和 slow 指针，从头结点出发，fast指针每次移动两个节点，slow指针每次移动一个节点，如果 fast 和 slow指针在途中相遇 ，说明这个链表有环

- fast指针一定先进入环中，如果fast指针和slow指针相遇的话，一定是在环中相遇，这是毋庸置疑的

- 其实相对于slow来说，fast是一个节点一个节点的靠近slow的

  ```
  /**
   * Definition for singly-linked list.
   * struct ListNode {
   *     int val;
   *     struct ListNode *next;
   * };
   */
  struct ListNode *detectCycle(struct ListNode *head) {
      struct ListNode* slow = head;
      struct ListNode* fast = head;
      while(fast && fast->next){
          slow = slow->next;
          fast = fast->next->next;
          if(slow == fast){
              struct ListNode *k = fast, *m = head;
              while (k != m){
                  k = k->next;
                  m = m->next;
              }
              return k;
          }
      }
      return NULL;
  }
  ```

  
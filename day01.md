### 数组理论基础

1. 数组是存放在连续内存空间上的相同类型数据的集合

2. 需要两点注意的是

   - **数组下标都是从0开始的**

   - **组内存空间的地址是连续的**

	因为数组在内存空间的地址是连续的，所以我们在删除或者增添元素的时候，就难免要移动其他元素的地址。（数组的元素是不能删的，只能覆盖）

### 704.二分查找

- 二分法的前提条件：有序数组；数组中无重复元素

- 边界条件：`while(left < right)/while(left <= right);right = middle/right = middle - 1`，写二分法经常写乱，主要是因为**对区间的定义没有想清楚，区间的定义就是不变量**。要在二分查找的过程中，保持不变量，就是在while寻找中每一次边界的处理都要坚持根据区间的定义来操作，这就是**循环不变量**规则。

  写二分法，区间的定义一般为两种，左闭右闭即[left, right]，或者左闭右开即[left, right)。
  
- 第一种写法：**target∈[left,right)]**
  
  ~~~
  int search(int* nums, int numsSize, int target) {
      int left = 0;
      int right = numsSize - 1;
      int middle = 0;
      while(left <= right)
      {
          middle = (left + right)/2; // middle = left + (right - left )/2;
          if(nums[middle] > target) {right = middle - 1;}
          else if(nums[middle] < target) {left = middle + 1;}
          else if(nums[middle] == target) {return middle;}
  
      }
      return -1;
  } 
  ~~~
  
- 第二种写法：**target∈[left,right)**
  
  ```
  int search(int* nums, int numsSize, int target) {
      int left = 0;
      int right = numsSize;
      int middle = 0;
      while(left < right)
      {
          middle = (left + right)/2; //middle = left + (right - left )/2;
          if(nums[middle] > target) {right = middle;}
          else if(nums[middle] < target) {left = middle + 1;}
          else if(nums[middle] == target) {return middle;}
  
      }
      return -1;
  } 

- `middle = (left + right)/2`与`middle = left + (right - left)/2`等效

- 本质上就是在循环条件中注意`left,right`与`middle`的关系，以及进入循环的初始条件（`right`与`numsSize`的关系）


### 27.移除元素

- 数组的元素在内存地址中是连续的，不能单独删除数组中的某个元素，只能覆盖。

- 暴力解法

  外循环遍历所有元素，当元素的值与目标值相同时进入内循环，内循环将后续元素前移一位。

  ```
  int removeElement(int* nums, int numsSize, int val) {
      for(int i = 0; i < numsSize; i++) //循环次数numsSize,判断每个数组元素
      {
          if(nums[i] == val) //数组元素值与目标值相同时，后续元素前移一位
          {    
              for(int j = i + 1; j<numsSize; j++) //判断内循环的次数：0·1······i·|i+1·i+2······numsSize-1|
              {
                  nums[j-1] = nums[j];
              }
              numsSize = numsSize - 1; //一次内循环后，剔除一个元素，numsSize减1
              i = i - 1; //一次内循环后，i位置元素值已更改，需将i的值回退1与外循环的i++抵消
          }
          
      }
      return numsSize;
  }
  ```

- 双指针法

  双指针法（快慢指针法）： **通过一个快指针和慢指针在一个for循环下完成两个for循环的工作**

  定义快慢指针
  
  - 快指针：寻找新数组的元素 ，新数组就是不含有目标元素的数组
  
  - 慢指针：指向更新后的新数组下标的位置
  
  数值相同时，快指针向后寻找新元素
  
  数值不同时，慢指针后移一位，快指针指向的元素值赋给慢指针指向的元素
  
  
  ```
  int removeElement(int* nums, int numsSize, int val) {
      int fast = 0;
      int slow = 0;
      for(fast; fast < numsSize; fast++) //数值相同时，仅fast加1，数值不同时，涉及slow及元素变化
      {
          if(nums[fast] != val)
          {
              nums[slow++] = nums[fast];
              // slow++;
              // nums[slow] = nums[fast];
          }
      }
      return slow;
  }
  ```
  
  

### 977.有序数组的平方 

- 暴力排序

  最直观的想法，莫过于：每个数平方之后，排个序

  **快排序**：

  - `qsort` 是 C 标准库中提供的一个函数，用于对数组进行快速排序。它在 `<stdlib.h>` 头文件中定义。`qsort` 使用的是快速排序算法，这是一种高效的排序算法，平均时间复杂度为 O(n log n)

  - 声明：`void qsort(void *base, size_t nitems, size_t size, int (*compar)(const void *, const void *));`

  - 参数：

    - `base`: 指向待排序数组的第一个元素的指针。
    
    - `nitems`: 数组中的元素数量。
    
    - `size`: 数组中每个元素的大小（以字节为单位）。
    
    - `compar`: 比较函数的指针，该函数用于比较两个元素。比较函数应当返回一个整数，表示比较结果：
    
      - 小于零：表示第一个元素小于第二个元素。
    
      - 等于零：表示两个元素相等。
    
      - 大于零：表示第一个元素大于第二个元素。  
  - 返回值：该函数不返回任何值。

  ```
  /**
   * Note: The returned array must be malloced, assume caller calls free().
   */
  int cmp(const void* _a, const void* _b)
  {
      int a = *(int*)_a, b = *(int*)_b;
      return a - b;
  }
  
  int* sortedSquares(int* nums, int numsSize, int* returnSize) {
      *returnSize = numsSize; //返回的数组大小就是原数组大小
      int* ans  = (int*)malloc(sizeof(int)*numsSize);
      for(int i = 0; i < numsSize; i++)
      {
          ans[i] = nums[i] * nums[i];
      }
      qsort(ans, numsSize, sizeof(int), cmp);
      return ans;
  }
  ```

- 双指针法

  数组平方后的最大值在两边，定义左右指针，再定义个新数组从右向左依次放置当前最大值
  
  ```
  /**
   * Note: The returned array must be malloced, assume caller calls free().
   */
  int* sortedSquares(int* nums, int numsSize, int* returnSize) {
      *returnSize = numsSize; //返回的数组大小就是原数组大小
      int left = 0;			//创建左右指针
      int right = numsSize - 1;
  
      int* ans = (int*)malloc(sizeof(int) * numsSize); //创建要返回的结果数组
      for(int k = numsSize - 1; k >= 0; k--)			 //k为结果数组下标
      {
          int lsquare = nums[left] * nums[left];
          int rsquare = nums[right] * nums[right];
          if(lsquare > rsquare)
          {
              ans[k] = lsquare;
              left++;
          }
          else
          {
              ans[k] = rsquare;
              right--;
          }
      }
      return ans;
  }
  ```
  
  

### 209.长度最小的子数组 

- 暴力解法

  外循环遍历整个数组，内循环找到满足和条件的子数组并判断长度

  ```
  #include <limits.h>
  int minSubArrayLen(int target, int* nums, int numsSize) {
      int minlength = INT_MAX; //#include <limits.h>
      int sum;
      for (int i = 0; i < numsSize; ++i)
      {
          sum = 0; //每次外循环设置sum为0
          for (int j = i; j < numsSize; ++j) //内循环初始值应为nums[i]
          {
              sum = sum + nums[j];
              if( sum >= target)
              {
                  int length = j - i + 1;
                  minlength = minlength < length ? minlength : length; 
                  //三目运算符 ？X：Y 如果条件为真 ? 则值为 X : 否则值为 Y
                  break;
              }
          }
      }
      return minlength == INT_MAX ? 0 : minlength;
  }
  
  ```

- 滑动窗口

  - 所谓滑动窗口，**就是不断的调节子序列的起始位置和终止位置，从而得出我们要想的结果**

  - 在本题中实现滑动窗口，主要确定如下三点：

    - 窗口内是什么？
    - 如何移动窗口的起始位置？
    - 如何移动窗口的结束位置？

    窗口就是满足其和 ≥ s 的长度最小的连续子数组。

    窗口的起始位置如何移动：如果当前窗口的值大于等于s了，窗口就要向前移动了（也就是该缩小了）。

    窗口的结束位置如何移动：窗口的结束位置就是遍历数组的指针，也就是for循环里的索引。

  - **滑动窗口的精妙之处在于根据当前子序列和大小的情况，不断调节子序列的起始位置。从而将O(n^2)暴力解法降为O(n)。**

  ```
  int minSubArrayLen(int target, int* nums, int numsSize) {
      int minlength = INT_MAX; //#include <limits.h>
      int sum = 0;
      int i = 0; //窗口起始位置
      for (int j = 0; j < numsSize; ++j) //窗口终止位置
      {
          sum += nums[j]; 
          while (sum >= target)
          {
              int length = j - i + 1;
              minlength = minlength < length ? minlength : length;
              sum -= nums[i++];
          }
  
      }
      return minlength == INT_MAX ? 0 : minlength;
  }
  ```
  
  

### 59.螺旋矩阵II

- **本题并不涉及到什么算法，就是模拟过程，但却十分考察对代码的掌控能力。**
- **循环不变量原则。**

```
/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
int** generateMatrix(int n, int* returnSize, int** returnColumnSizes) {
    *returnSize = n;
    *returnColumnSizes = (int*)malloc(sizeof(int) * n); //returnColumnSizes为指向一维数组的指针

    int** ans = (int**)malloc(sizeof(int*) * n);
    for (int i = 0; i < n; ++i)
    {
        ans[i] = (int*)malloc(sizeof(int) * n);
        (*returnColumnSizes)[i] = n;
    }

    int startX = 0; //每次循环的起始位置
    int startY = 0; //每次循环的起始位置
    int offset = 1; //每次循环的偏移量
    int mid = n/2; //用于最后一个元素
    int count = 1; 
    int loop = n/2;
    while(loop)
    {
        int i = startX;
        int j = startY;
        for (; j < n - offset; j++)
        {
            ans[startX][j] = count++;
        }
        for ( ; i < n - offset; i++)
        {
            ans[i][j] = count++;
        }
        for (; j > startY ; j--)
        {
            ans[i][j] = count++;
        }
        for (; i > startX; i--)
        {
            ans[i][j] = count++;
        }

        offset ++;
        startX ++;
        startY ++;
        loop--;
    }
    if(n%2)
    {
        ans[mid][mid] = count;
    }
    return ans;
}

```


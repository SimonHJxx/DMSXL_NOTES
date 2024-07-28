### 哈希表理论基础

- 首先什么是哈希表，哈希表（英文名字为Hash table，国内也有一些算法书籍翻译为散列表，大家看到这两个名称知道都是指hash table就可以了）
- **哈希表是根据关键码的值而直接进行访问的数据结构**
- **一般哈希表都是用来快速判断一个元素是否出现集合里**
- **哈希函数**
- **哈希碰撞**
- **我们遇到了要快速判断一个元素是否出现集合里的时候，就要考虑哈希法**
- 哈希法是**牺牲了空间换取了时间**

### 24. 两两交换链表中的节点

- 

  ```
  bool isAnagram(char* s, char* t) {
      // 先判断两字符长度是否相同
      int lens = strlen(s);
      int lent = strlen(t);
      if(lent != lens) return false;
      // 分配两个数组，存储每个字符串对应字符出现的次数
      int map1[26] = {0};
      int map2[26] = {0};
      for (int i = 0; i < lens; ++i) { //循环次数使用字符串长度更节省时间
          map1[s[i] - 'a'] += 1;
          map2[t[i] - 'a'] += 1;
      }
      for (int i = 0; i < 26; ++i) {
          if(map1[i] != map2[i]) return false;
      }
      return true;
  } 
  ```

### 349. 两个数组的交集

- 1 <= nums1.length，nums2.length <= 1000

- 0 <= nums1[i], nums2[i] <= 1000

  ```
  /**
   * Note: The returned array must be malloced, assume caller calls free().
   */
  int* intersection(int* nums1, int nums1Size, int* nums2, int nums2Size, int* returnSize) {
      // 哈希数组
      int nums1Cnt[1001] = {0};
      // 返回的数组result,大小为lessSize
      int lessSize = nums1Size < nums2Size ? nums1Size : nums2Size;
      int *result = (int *)calloc(lessSize,sizeof (int));
      int resultIndex = 0;
      int i = 0;
      // nums1的值作为nums1Cnt的索引值
      for (i = 0; i < nums1Size; i++) {
          nums1Cnt[nums1[i]]++;
      }
      // 若nums2作为nums1Cnt的索引值大于0，则将nums1Cnt的索引值传入result数组
      for (i = 0; i < nums2Size; ++i) {
          if (nums1Cnt[nums2[i]] > 0){
              result[resultIndex] = nums2[i];
              resultIndex++;
              // 将nums1Cnt的索引值清0，避免nums2的元素重复计算
              nums1Cnt[nums2[i]] = 0;
          }
      }
      *returnSize = resultIndex;
      return result;
  }
  ```



### 202. 快乐数

- quot为除式的商，rem为除式的余数

  > typedef struct _div_t {
  >   int quot;
  >   int rem;
  >
  > } div_t;

- div() 函数的声明
  > div_t div(int numer, int denom) // numer -- 分子,denom -- 分母
  
  ```
  #include <stdlib.h>
  int getsum (int n){
      int sum = 0;
      div_t n_div = { .quot = n};
      while(n_div.quot != 0){
          n_div = div(n_div.quot, 10);
          sum += n_div.rem * n_div.rem;
      }
      return sum;
  }
  
  bool isHappy(int n) {
      int slow = n , fast = n;
      do {
          slow = getsum(slow);
          fast = getsum(getsum(fast));
      }while(slow != fast);
      
      return (fast == 1);
  }
  ```
  
  

### 1. 两数之和

- **key来存元素，value来存下标**

  ```
  /**
   * Note: The returned array must be malloced, assume caller calls free().
   */
  
  typedef struct {
      int key;
      int value;
      UT_hash_handle hh;
  } map;
  
  map *hashMap = NULL;
  
  void hashMapAdd(int key, int value) {
      map *s;
      HASH_FIND_INT(hashMap, &key, s);
      if(s == NULL){
          s = (map*)malloc(sizeof(map));
          s -> key = key;
          HASH_ADD_INT(hashMap, key, s);
      }
      s -> value = value;
  }
  
  map* hashMapFind(int key) {
      map* s;
      HASH_FIND_INT(hashMap, &key, s);
      return s;
  }
  
  void hashMapCleanup(){
      map *cur, *tmp;
      HASH_ITER(hh, hashMap, cur, tmp){
          HASH_DEL(hashMap, cur);
          free(cur);
      }
  }
  
  void hashPrint(){
      map* s;
      for (s = hashMap; s != NULL; s =(map*)(s -> hh.next)) {
          printf("key %d, value %d\n", s -> key, s -> value);
      }
  }
  
  
  int* twoSum(int* nums, int numsSize, int target, int* returnSize) {
      int i, *ans;
      map *hashMapRes;
      hashMap = NULL;
      ans = malloc(sizeof(int) * 2);
  
      for (i = 0; i < numsSize; ++i) {
          hashMapAdd(nums[i], i);
      }
  
      hashPrint();
  
      for (i = 0; i < numsSize; i++) {
          hashMapRes = hashMapFind(target - nums[i]);
          if(hashMapRes && hashMapRes -> value != i){
              ans[0] = i;
              ans[1] = hashMapRes -> value;
              *returnSize = 2;
              return ans;
          }
      }
  
      hashMapCleanup();
      return NULL;
  
  }
  ```

  

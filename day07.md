### 454.四数相加II

- 分组+哈希表

  ```
  
  
  struct hashTable{
      int key;
      int val;
      UT_hash_handle hh;
  };
  // tmp -> val用于存放和相同的组的个数
  int fourSumCount(int* nums1, int nums1Size, int* nums2, int nums2Size, int* nums3, int nums3Size, int* nums4, int nums4Size){
      struct hashTable* hashtable = NULL;
      for (int i = 0; i < nums1Size; ++i) {
          for (int j = 0; j < nums2Size; ++j) {
              int ikey = nums1[i] + nums2[j];
              struct hashTable* tmp;
              HASH_FIND_INT(hashtable, &ikey, tmp);
              if (tmp == NULL){
                  struct hashTable* tmp = malloc(sizeof(struct hashTable));
                  tmp -> key = ikey;
                  tmp -> val = 1;
                  HASH_ADD_INT(hashtable, key, tmp);
              }
              else{
                  tmp -> val++;
              }
          }
      }
  
      int ans = 0;
      for (int i = 0; i < nums3Size; ++i) {
          for (int j = 0; j < nums4Size; ++j) {
              int ikey = -nums3[i] - nums4[j];
              struct hashTable* tmp;
              HASH_FIND_INT(hashtable, &ikey, tmp);
              if(tmp != NULL){
                  ans += tmp -> val;
              }
          }
      }
      return ans;
  }
  ```

  

### 383. 赎金信

- 

  ```
  bool canConstruct(char* ransomNote, char* magazine) {
      int hashmap[26] = {0};
      while(*magazine != '\0'){
          hashmap[*magazine - 'a']++;
          magazine++;
      }
      while (*ransomNote != '\0'){
          hashmap[*ransomNote - 'a']--;
          ransomNote++;
      }
      for (int i = 0; i < 26; ++i) {
          if(hashmap[i] < 0){
              return false;
          }
      }
      return true;
  }
  ```

  

### 15. 三数之和

- 

  ```
  /**
   * Return an array of arrays of size *returnSize.
   * The sizes of the arrays are returned as *returnColumnSizes array.
   * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
   */
  
  int cmp(const void* ptr1, const void* ptr2) {
      return *((int*)ptr1) > *((int*)ptr2);
  }
  
  
  int** threeSum(int* nums, int numsSize, int* returnSize, int** returnColumnSizes) {
      int** ans = (int**)malloc(sizeof(int*) * 18000);
      int ansTop = 0;
      if(numsSize < 3){
          *returnSize = 0;
          return ans;
      }
  
      qsort(nums, numsSize, sizeof(int), cmp);
  
      int i;
      for (i = 0; i < numsSize; i++) {
          if(nums[i] > 0){
              break;
          }
          if(i > 0 && nums[i] == nums[i - 1]){
              continue;
          }
  
          int left = i + 1;
          int right = numsSize - 1;
  
          while (right > left){
              int sum = nums[i] + nums[left] + nums[right];
              if(sum < 0) left ++;
              else if(sum >0) right --;
              else{
                  int* arr = (int*)malloc(sizeof(int) * 3);
                  arr[0] = nums[i];
                  arr[1] = nums[left];
                  arr[2] = nums[right];
                  ans[ansTop++] = arr;
                  while(right > left &&nums[right] == nums[right - 1]){
                      right --;
                  }
                  while (left < right && nums[left] == nums[left + 1]){
                      left ++;
                  }
                  right --;
                  left ++;
              }
          }
      }
  
      *returnSize = ansTop;
      *returnColumnSizes = (int*)malloc(sizeof(int) * ansTop);
      int z;
      for (z = 0; z < ansTop; z++) {
          (*returnColumnSizes)[z] = 3;
      }
  
      return ans;
  
  }
  ```

  


### 18. 四数之和 

- 

  ```
  /**
   * Return an array of arrays of size *returnSize.
   * The sizes of the arrays are returned as *returnColumnSizes array.
   * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
   */
  
  int cmp(const void *a, const void *b) {
      return *((int*)a) > *((int*)b);
  }
  
  int** fourSum(int* nums, int numsSize, int target, int* returnSize, int** returnColumnSizes) {
      qsort(nums, numsSize, sizeof(int), cmp);
      int** res = (int*)malloc(sizeof(int*) * 40000);
      int index = 0;
  
      for (int k = 0; k < numsSize - 3; ++k) {
          if((nums[k] > target) && (nums[k] >= 0)){
              break;
          }
          if((k > 0) && (nums[k] == nums[k - 1])){
              continue;
          }
  
          for (int i = k + 1; i < numsSize - 2; ++i) {
              if((nums[k] + nums[i] > target) && (nums[i] >= 0)){
                  break;
              }
              if((i > (k + 1)) && (nums[i] == nums[i - 1])){
                  continue;
              }
  
              int left = i + 1;
              int right = numsSize - 1;
              while(left < right){
                  long long val = (long long)nums[k] + nums[i] + nums[left] + nums[right];
                  if(val > target) right--;
                  else if(val < target) left++;
                  else{
                      int* res_tmp = (int*)malloc(sizeof(int) * 4);
                      res_tmp[0] = nums[k];
                      res_tmp[1] = nums[i];
                      res_tmp[2] = nums[left];
                      res_tmp[3] = nums[right];
                      res[index++] = res_tmp;
  
                      while((right > left) && (nums[right] == nums[right - 1])) right--;
                      while ((left < right) && (nums[left] == nums[left + 1])) left++;
                      right--;
                      left++;
                  }
              }
          }
      }
      *returnSize = index;
      *returnColumnSizes  = (int*)malloc(sizeof(int) * index);
      for (int i = 0; i < index; ++i) {
          (*returnColumnSizes)[i] = 4;
      }
  
          return res;
  }
  ```
  
  
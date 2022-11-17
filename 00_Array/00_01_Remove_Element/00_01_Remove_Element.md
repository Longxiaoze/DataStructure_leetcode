# 数组的元素删除问题


## 1）[27. 移除元素](https://leetcode.cn/problems/remove-element/)  [27. Remove Element](https://leetcode.com/problems/remove-element/) 

题解：给定一个整数数组nums和一个整数val，删除所有出现的val的地方，返回删除后的数组长度

标准的双指针解法：O(n)，O(1)
```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int slowIndex = 0;
        for (int fastIndex = 0; fastIndex < nums.size(); fastIndex++) {
            if (val != nums[fastIndex]) {
                nums[slowIndex] = nums[fastIndex];
                slowIndex +=1;
            }
        }
        return slowIndex;
    }
};
```

改进版，加了一些case来处理开头如果不相等的情况
```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int slowIndex = 0;
        for (int fastIndex = 0; fastIndex < nums.size(); fastIndex++) {
            if (val != nums[fastIndex] &&slowIndex!=fastIndex) {
                nums[slowIndex] = nums[fastIndex];
                slowIndex +=1;
            }
            else if (val != nums[fastIndex] &&slowIndex==fastIndex){
                slowIndex +=1;
            }
        }
        return slowIndex;
    }
};
```



## 2）[26.删除排序数组中的重复项](https://leetcode.cn/problems/remove-duplicates-from-sorted-array/)  [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

题解：给定一个递增排序的整数数组nums，删除重复项，使每个唯一元素只出现一次。元素的相对顺序应该保持不变。返回最终的数组长度。

```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums)
    {
       if(nums.size()==0) return 0;
       int slowIndex =0;
       for(int fastIndex=1;fastIndex<nums.size();fastIndex++)
       {
           if(nums[slowIndex]!=nums[fastIndex])
           {
               slowIndex++;
               nums[slowIndex]=nums[fastIndex];
           }
       } 
       return slowIndex+1;
       
    }
};
```

## 3）[283.移动零](https://leetcode.cn/problems/move-zeroes/)  [283. Move Zeroes](https://leetcode.com/problems/move-zeroes/)

题解：

```cpp

```

## 4）[844.比较含退格的字符串](https://leetcode.cn/problems/backspace-string-compare/)  [844. Backspace String Compare](https://leetcode.com/problems/backspace-string-compare/)

题解：

```cpp

```

## 5）[977.有序数组的平方](https://leetcode.com/problems/squares-of-a-sorted-array/)  [977. Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/)

题解：
```cpp

```

# 总结


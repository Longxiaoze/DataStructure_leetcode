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

题解：给定一个整数数组nums，将所有的0移动到到末尾，同时保持非零元素的相对顺序。

```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int slowIndex = 0;
        int flag;
        for (int fastIndex = 0; fastIndex < nums.size(); fastIndex++) {
            if (nums[fastIndex] != 0) {
                flag = nums[slowIndex];
                nums[slowIndex] = nums[fastIndex];
                nums[fastIndex] = flag;
                slowIndex +=1;
                 }
        }
    }    
};

```

## 4）[844.比较含退格的字符串](https://leetcode.cn/problems/backspace-string-compare/)  [844. Backspace String Compare](https://leetcode.com/problems/backspace-string-compare/)

题解：给定 s 和 t 两个字符串，当它们分别被输入到空白的文本编辑器后，如果两者相等，返回 true 。# 代表退格字符。

```cpp
class Solution {
public:
    bool backspaceCompare(string S, string T) {
        int i = S.size() - 1, j = T.size() - 1, countA = 0, countB = 0;
        while(i >= 0 || j >= 0){
            while(i >= 0 && (S[i] == '#' || countA > 0))
                if(S[i--] == '#'){++countA;} else{--countA;}
            while(j >= 0 && (T[j] == '#' || countB > 0)) 
                if(T[j--] == '#'){++countB;} else{--countB;}
            if(i < 0 || j < 0) return i == j;
            if(S[i--] != T[j--]) return false;
        }
        return i == j;
    }
};
```

## 5）[977.有序数组的平方](https://leetcode.com/problems/squares-of-a-sorted-array/)  [977. Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/)

题解：
```cpp
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        vector<int> res(nums.size());
        int l = 0, r = nums.size() - 1;
        for (int k = nums.size() - 1; k >= 0; k--) {
            if (abs(nums[r]) > abs(nums[l])) {
                res[k] = nums[r] * nums[r];
                r--;
            }
            else {
                res[k] = nums[l] * nums[l];
                l++;
            }
        }
        return res;
    }
};
```

# 总结
对于数组的双指针问题，通常可以用来解决数组改变的问题，或者两个数组之间进行比较的问题。

如[1）[27. 移除元素]](https://github.com/Longxiaoze/DataStructure_leetcode/blob/main/00_Array/00_01_Remove_Element/00_01_Remove_Element.md#127-%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0--27-remove-element)一题，就是最经典的双指针修改数组的问题。

如[2）[26.删除排序数组中的重复项]](https://github.com/Longxiaoze/DataStructure_leetcode/blob/main/00_Array/00_01_Remove_Element/00_01_Remove_Element.md#226%E5%88%A0%E9%99%A4%E6%8E%92%E5%BA%8F%E6%95%B0%E7%BB%84%E4%B8%AD%E7%9A%84%E9%87%8D%E5%A4%8D%E9%A1%B9--26-remove-duplicates-from-sorted-array)[3）[283.移动零]](https://github.com/Longxiaoze/DataStructure_leetcode/blob/main/00_Array/00_01_Remove_Element/00_01_Remove_Element.md#3283%E7%A7%BB%E5%8A%A8%E9%9B%B6--283-move-zeroes)[5）[977.有序数组的平方]](https://github.com/Longxiaoze/DataStructure_leetcode/blob/main/00_Array/00_01_Remove_Element/00_01_Remove_Element.md#5977%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84%E7%9A%84%E5%B9%B3%E6%96%B9--977-squares-of-a-sorted-array)三个题目，就是很经典的修改单个数组的问题。这三个题目中[2）[26.删除排序数组中的重复项]](https://github.com/Longxiaoze/DataStructure_leetcode/blob/main/00_Array/00_01_Remove_Element/00_01_Remove_Element.md#226%E5%88%A0%E9%99%A4%E6%8E%92%E5%BA%8F%E6%95%B0%E7%BB%84%E4%B8%AD%E7%9A%84%E9%87%8D%E5%A4%8D%E9%A1%B9--26-remove-duplicates-from-sorted-array)和[3）[283.移动零]](https://github.com/Longxiaoze/DataStructure_leetcode/blob/main/00_Array/00_01_Remove_Element/00_01_Remove_Element.md#3283%E7%A7%BB%E5%8A%A8%E9%9B%B6--283-move-zeroes)都是双指针从同一侧移动的题目。[5）[977.有序数组的平方]](https://github.com/Longxiaoze/DataStructure_leetcode/blob/main/00_Array/00_01_Remove_Element/00_01_Remove_Element.md#5977%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84%E7%9A%84%E5%B9%B3%E6%96%B9--977-squares-of-a-sorted-array)一题则是双指针从两侧向中间移动的题目。

如[4）[844.比较含退格的字符串]](https://github.com/Longxiaoze/DataStructure_leetcode/blob/main/00_Array/00_01_Remove_Element/00_01_Remove_Element.md#4844%E6%AF%94%E8%BE%83%E5%90%AB%E9%80%80%E6%A0%BC%E7%9A%84%E5%AD%97%E7%AC%A6%E4%B8%B2--844-backspace-string-compare)一题则是两个数组进行比较的问题，指针分别在两个字符串(也就是数组移动比较)。

1）2）3）都是对本身数组进行修改，5）新建了一个数组，多了一部分的内存，进一步可以考虑优化内存。

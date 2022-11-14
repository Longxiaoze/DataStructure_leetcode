# 数组中二分查找的题目


## 1）[704.二分查找](https://leetcode.cn/problems/binary-search/)  [704.binary-search](https://leetcode.com/problems/binary-search/) 

题解：最经典的二分查找nums是升序无重复数组，target是在nums中搜索的数字，要求返回查找的index，没有找到返回-1。

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left  = 0;
        int right  = nums.size()-1;
        
        while(left<=right){
            int middle = left + (right-left)/2;
            if (nums[middle]>target){
                right = middle-1;
            }
            else if (nums[middle]<target){
                left = middle+1;
            }
            else return middle;
        }
        return -1;
    }
};
```

## 2）[35.搜索插入位置](https://leetcode.cn/problems/search-insert-position/)  [35. Search Insert Position](https://leetcode.com/problems/search-insert-position/)

题解：给定一个由不同整数组成的排序数组和一个目标值，如果找到目标，则返回索引。如果不是，则返回按顺序插入的索引。无重复。

```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int left= 0 ,right= nums.size()-1 ;
        while(left <= right){
            int mid= left + (right- left)/2 ;
            if(nums[mid] == target){
                return mid ;
            }
            else if(nums[mid] > target){
                right= mid -1 ;
            }
            else{
                left= mid + 1 ;
            }
        }
		// Edge Case
        return left ;
    }
};
```

## 3）[34.在排序数组中查找元素的第一个和最后一个位置](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/)  [34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

题解：nums给定一个按非降序排序的整数数组，找到给定target值的开始和结束位置。如果target在数组中找不到，则返回[-1, -1]。递增数组。

```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        vector<int> solution;
        int left = 0, right = nums.size()-1;
        int mid;
        int i = -1; // return index
        int j = -1;
        
        while(left <= right){
            mid = (right + left) / 2;
            if(target < nums[mid]){
                right = mid - 1;
            }
            else if(target > nums[mid]){
                left = mid+1;
            }
            else if(target == nums[mid]){
                /* MODIFY to find lower and upper bounds */
                i = mid;
                j = mid;
                while(nums[i] == target && i != 0 ){                
                    if(nums[i-1] == target){ 
                        i = i-1;
                }
                    else break;}
                while(nums[j] == target && j != nums.size()-1){                
                    if(nums[j+1] == target){
                        j = j+1;
                }
                    else break;}
                break;
            }
        }
        solution.push_back(i);
        solution.push_back(j);
        return solution;
    }
};
```

## 4）[69.x 的平方根](https://leetcode.cn/problems/sqrtx/)  [69. Sqrt(x)](https://leetcode.com/problems/sqrtx/)

题解：给定一个非负整数x，返回向下舍入到最接近的整数，如输入8返回2。返回的整数也应该是非负的。

```cpp
class Solution {
public:
	int mySqrt(int x) {
		int left=0, right=x, ans;
		while(left<=right){
			long long int mid=left+(right-left)/2;
			if(mid*mid==x)return mid;
			else if(mid*mid<x) left=mid+1;
			else right=mid-1;
		}
		return ans;
	}
};
```

## 5）[367.有效的完全平方数](https://leetcode.cn/problems/binary-search/)  [367. Valid Perfect Square](https://leetcode.com/problems/valid-perfect-square/)

题解：给定一个正整数num，编写一个函数，如果num是完全平方则返回 True ，否则返回 False 。

```cpp
class Solution {
public:
    bool isPerfectSquare(int num) {
        int left = 1,right = num;
        while(left<=right){
            int middle = left+(right-left)/2;
            if (num%middle==0 && middle == num/middle) return true;
            else if (middle<num/middle) left = middle+1;
            else right = middle-1;
        }
        return false;
    }
};
```

# 总结
1）[704.二分查找](https://github.com/Longxiaoze/DataStructure_leetcode/blob/main/00_Array/00_00_BinarySearch/00_00_BinarySearch.md#1704%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE--704binary-search)是最经典的二分查找的解题思路，不过需要注意，一般二分查找的区间设定可以左闭右闭，也就是[i,j]。也有一种写法是左闭右开，可以参考[二分查找](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.md)。二分查找，从名字可以知道这是一个用来查找的算法，那么也就是说，这是一个可以从数组中查找指定位置的算法。后面的所有题基本上都沿着查找这个思路进行了一定程度的修改。

如2）[35.搜索插入位置](https://github.com/Longxiaoze/DataStructure_leetcode/blob/main/00_Array/00_00_BinarySearch/00_00_BinarySearch.md#235%E6%90%9C%E7%B4%A2%E6%8F%92%E5%85%A5%E4%BD%8D%E7%BD%AE--35-search-insert-position)一题，查找的是指定位置，没有找到的时候需要返回距离查找最小的那个**位置**。也就是代码中的return left;

如3）[34.在排序数组中查找元素的第一个和最后一个位置](https://github.com/Longxiaoze/DataStructure_leetcode/blob/main/00_Array/00_00_BinarySearch/00_00_BinarySearch.md#334%E5%9C%A8%E6%8E%92%E5%BA%8F%E6%95%B0%E7%BB%84%E4%B8%AD%E6%9F%A5%E6%89%BE%E5%85%83%E7%B4%A0%E7%9A%84%E7%AC%AC%E4%B8%80%E4%B8%AA%E5%92%8C%E6%9C%80%E5%90%8E%E4%B8%80%E4%B8%AA%E4%BD%8D%E7%BD%AE--34-find-first-and-last-position-of-element-in-sorted-array)一题，从中间查找指定位置的同时，还需要检测**区间的最左边和最右边的位置**。只不过对于二分法来说，能检测到指定的值，但是区间左右两边需要另外写代码来检测，因此，我们可以发现，对于该题目来说，else if(target == nums[mid])只有这里的需要修改来检测区间左右两边。

如4）[69.x 的平方根](https://github.com/Longxiaoze/DataStructure_leetcode/blob/main/00_Array/00_00_BinarySearch/00_00_BinarySearch.md#469x-%E7%9A%84%E5%B9%B3%E6%96%B9%E6%A0%B9--69-sqrtx)一题，二分查找同样用来找数组中指定的值

如 5）[367.有效的完全平方数](https://github.com/Longxiaoze/DataStructure_leetcode/blob/main/00_Array/00_00_BinarySearch/00_00_BinarySearch.md#5367%E6%9C%89%E6%95%88%E7%9A%84%E5%AE%8C%E5%85%A8%E5%B9%B3%E6%96%B9%E6%95%B0--367-valid-perfect-square)一题，与4）基本相同，但是需要注意的是，如果我们不想使用乘法，因为乘法可能超出界限，我们可以换一种思路使用除法来进行替换，从而避免使用longlong和超界的问题，即使用num%middle==0 && middle == num/middle来替换middle*middle == num。

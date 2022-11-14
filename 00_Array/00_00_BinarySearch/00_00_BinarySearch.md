# 数组中二分查找的题目


1）[704.二分查找](https://leetcode.cn/problems/binary-search/)  [704.binary-search](https://leetcode.com/problems/binary-search/) 

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

2）[35.搜索插入位置](https://leetcode.cn/problems/search-insert-position/)  [35. Search Insert Position](https://leetcode.com/problems/search-insert-position/)

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

3）[34.在排序数组中查找元素的第一个和最后一个位置](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/)  [34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

题解：nums给定一个按非降序排序的整数数组，找到给定target值的开始和结束位置。如果target在数组中找不到，则返回[-1, -1]。递增数组。

```cpp
class Solution {
public:
    
    /*
    Call binary search twice to find upper and lower bound.
    Runtime: O(log n) since it's 2 * O(log n)
    */
    vector<int> searchRange(vector<int>& nums, int target) {
        vector<int> solution;
        int left = binarySearch(nums, target, true);
        int right = binarySearch(nums, target, false);
        solution.push_back(left);
        solution.push_back(right);
        return solution;
    }
    
    /* 
    boolean leftSearch indicates we're looking for left boundary.
    if false, we are looking for right boundary.
    */
    int binarySearch(vector<int>&nums, int target, bool leftSearch){
        int left = 0, right = nums.size()-1;
        int mid;
        int i = -1; // return index
        
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
                if(leftSearch){ // IF lower bound
                    right = mid-1;
                }
                else{ // IF upper bound
                    left = mid+1; 
                }
            }
        }
        return i;
    }
};
```

4）[69.x 的平方根](https://leetcode.cn/problems/sqrtx/)  [69. Sqrt(x)](https://leetcode.com/problems/sqrtx/)

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

5）[367.有效的完全平方数](https://leetcode.cn/problems/binary-search/)  [367. Valid Perfect Square](https://leetcode.com/problems/valid-perfect-square/)

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
1）[704.二分查找]是最经典的二分查找的解题思路，不过需要注意，一般二分查找的区间设定可以左闭右闭，也就是[i,j]。也有一种写法是左闭右开，可以参考[二分查找](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.md)。二分查找，从名字可以知道这是一个用来查找的算法，那么也就是说，这是一个可以从数组中查找指定位置的算法。后面的所有题基本上都沿着查找这个思路进行了一定程度的修改。

如2）[35.搜索插入位置]一题

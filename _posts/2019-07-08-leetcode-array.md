---
layout: post
title: lc-array1-easy-1,26,27
date: 2019-07-08 22:00:11.000000000 +09:00
tags: array,leetcode
---

# 1. [two sum](https://leetcode.com/problems/two-sum/description/)
Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
***
>题述：
>给出一个**整数组成的数组**，**找出和等于某一特定值的两个元素的下标**，题目保证有唯一输出。

***

## 1.1.1 python solution1：运用python字典结构

* 遍历数组（第一个数），算余值（求第二个数）；
* 将遍历过数和下标构建字典；
* 查询第二个数是否在字典中；
* 最多遍历一遍，便能找到余值，并返回两个数的下标。

```python
class solution():
   def twoSum(self, nums, target):
       """
       :type nums: List[int]
       :type target: int
       :rtype: List[int]
       """
       hash = {}
       for i in range(len(nums)):
           if target - nums[i] in hash:
               return [i, hash[target - nums[i]]]
           else:
               hash[nums[i]] = i

       #无解时
       return [-1, -1]
```

* 注意返回值的格式；
* 注意括号的完整性；
* 注意python字典取值格式；
* 注意python字典的： key:word对；
***

## 1.1.2 python solution2：运用Python数组的index方法
* 遍历数组，计算另一数；
* 用 `in` 方法查询第二个数是否在数组中；
* 用`.index`方法查询该数在数组中的下标；

```python
class Solution(object):
   def twoSum(self, nums, target):
       """
       :type nums: List[int]
       :type target: int
       :rtype: List[int]
       """
       for i in range(0,len(nums)):
           if (target - nums[i]) in nums[i+1:]:
               return [i, nums.index(target - nums[i], i+1, len(nums))]
```

* `in`方法
* python数组的`.index`方法

***


## 1.2.1 C++ solution1: 运用hash函数

```C++
vector<int> twoSum(vector<int> &numbers, int target)
{
   //Key is the number and value is its index in the vector.
       unordered_map<int, int> hash;
       vector<int> result;
       for (int i = 0; i < numbers.size(); i++) {
               int numberToFind = target - numbers[i];

           //if numberToFind is found in map, return them
               if (hash.find(numberToFind) != hash.end()) {
                   //+1 because indices are NOT zero based
                       result.push_back(hash[numberToFind]);
                       result.push_back(i);                  
                       return result;
               }

           //number was not found. Put it in the map.
               hash[numbers[i]] = i;
       }
       return result;
}
```
* `vector<int> result`：结果用vector表示；
* `map<int, int> hash`：构建空的哈希map；
* `for(int i = 0; i < 10; i++){  }`：遍历数组下标；
* `number.size()`：取得vector的大小；
* `if hash.find（numberToFind) != hash.end(){  }`:如果hash表中能找到第二个数；
* `result.push_back()`：向vector 中推入某数；

# 26. [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)

Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

Example 1:

```
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
```
Example 2:

```
Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.
```
Clarification:

Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by reference, which means modification to the input array will be known to the caller as well.

Internally you can think of this:

```
// nums is passed in by reference. (i.e., without making a copy)
int len = removeDuplicates(nums);

// any modification to nums in your function would be known by the caller.
// using the length returned by your function, it prints the first len elements.
for (int i = 0; i < len; i++) {
   print(nums[i]);
}
```

>对一个已排序了的数组，进行去重操作，返回最后的长度：
>>**空间复杂度要求**：O(1)

## 26.1.1 python solution1:遍历法 + 双指针法
* 定义**一个start指针** 和 **一个工作指针**；
* 不一样，存储工作指针下的元素到start指针下，并接力挪位start指针；
* 一样，则后移工作指针；
* 返回最后数组的长度（即**start指针的值 + 1**）

```python
def removeDuplicates(self, nums):
   """
   :type nums: List[int]
   :rtype: int
   """
   if not nums:    #因为nums可能为[]
       return 0
   start = 0

   for i in range(1, len(nums)):        #i即工作指针，工作指针遍历原数组，遍历完一个后即可扔掉
       if nums[start] == nums[i]:       #start为存储指针，存储指针恰好处于被扔掉的区域
      #     i += 1
       else:
           start += 1                   #找到新的尾巴
           nums[start] = nums[i]        #则存储
   return start+1
```

* `if not nums: `:判断list是否为空（**注意算法完备性**）

## 26.2.1 C++ Solution:互斥思想
* 遍历数组，计算数组中，重复元素的个数count，最后用总个数减掉count;
* 后面一个数，等于前面的数，则count + 1;

```C++
int count = 0;
for(int i = 1; i < n; i++){
   if(A[i] == A[i-1]) count++;
   else A[i-count] = A[i];
}
return n-count;
```

# [27. Remove Element](https://leetcode.com/problems/remove-element/description)

Given an array nums and a value val, remove all instances of that value in-place and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

Example 1:

```
Given nums = [3,2,2,3], val = 3,

Your function should return length = 2, with the first two elements of nums being 2.

It doesn't matter what you leave beyond the returned length.
```
Example 2:

```
Given nums = [0,1,2,2,3,0,4,2], val = 2,

Your function should return length = 5, with the first five elements of nums containing 0, 1, 3, 0, and 4.

Note that the order of those five elements can be arbitrary.

It doesn't matter what values are set beyond the returned length.
```
Clarification:

Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by reference, which means modification to the input array will be known to the caller as well.

Internally you can think of this:

```
// nums is passed in by reference. (i.e., without making a copy)
int len = removeElement(nums, val);

// any modification to nums in your function would be known by the caller.
// using the length returned by your function, it prints the first len elements.
for (int i = 0; i < len; i++) {
   print(nums[i]);
}
```

>给出一个数组，和一个数，去掉数组中所有的该数
>>空间复杂度要求:O(1);
>>数组中元素循序不作要求。

## 27.1.1 python solution1:首尾双指针法

* 首位各一个指针；
* 从头指针开始，若该指针下的数需删除，则移到后面去（与尾指针交换）；
* 否则首指针后移，直至首位指针重合；
* 返回的长度值即首指针的位置。


```python
def removeElement(self, nums, val):
   start, end = 0, len(nums) - 1
   while start <= end:
       if nums[start] == val:
           nums[start], nums[end], end = nums[end], nums[start], end - 1    #将当前数与最后一个数交换，并将工作区的末尾前移一位
       else:
           start +=1              #工作区的头指针后移一位
   return start
```

* 注意**返回值的精确值**：需画图或带入数值进行计算确认
* Python中：元素交换的写法：`nums[start], nums[end] = nums[end], nums[start]`

## 27.1.2 python solution2:运用python的高级函数


```python
class Solution(object):
   def removeElement(self, nums, val):
       for i in range(nums.count(val)):    #在一个列表list中对某一值进行计数
           nums.remove(val)                #在一个列表list中去掉某一值（第一个）
       return len(nums)
```

* `list_data.count(val)`：python的list计数函数；
* `nums.remove(val)`: python的list删除函数；


## 27.2.1 c++ solution1:数组筛检映射法

* 定义工作指针（新数组）和遍历指针（旧数组）；
* 将（遍历指针下）满足条件的元素移到新数组中（工作指针下的元素）。

```c++
class Solution {
public:
   int removeElement(vector<int>& nums, int val) {
       int len = 0;
       for(int i = 0; i < nums.size(); i++) {
           if(nums[i] != val) {
               nums[len++] = nums[i];
           }
       }
       return len;
   }
};
```

* `vector_nums.size()`:容器的大小；
* 注意最后指针的位置。

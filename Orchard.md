# 一. Remove Element

> Given an array and a value, remove all instances of that value in place and return the new length. The order of elements can be changed. It does't matter what you leave beyond the new length.

要求：在一个数组里移除指定value，并且返回新的数组长度。因为题目里面要求了in place，所以我们还不能新建数组。

## 1.solution:
```C++
#include <iostream>
using namespace std;

class Solution
{
public:
	int removeElement(int a[], int n, int element);
};

int Solution::removeElement(int a[], int n, int element)
{
	int i = 0, j = 0;
	for(; i < n; i++)
	{
		if(a[i] == element)
		{
			continue;
		}
		else
		{
			a[j] = a[i];
			j++;
		}
	}
	return j;
}

int main()
{
	int a[6] = {1,2,2,3,2,4};
	int size = 6;
	int element = 2;
	Solution b;
	cout << "处理前数组的长度为" << size << "数组的内容为";
	for(int i = 0; i < size; i++)
	{
		cout << a[i] << " ";
	}
	int result = b.removeElement(a,size,element);
	cout << endl << "处理后数组的长度为" << result << "数组的内容为";
	for(int j = 0; j < result; j++)
	{
		cout << a[j] << " ";
	}
}
```
## 2.Analysis

创建了Solution类，包含了解决函数removeElement(int a[], int size, int element),其中函数的输入参数分别为“数组”、“数组长度”和“需要移除的元素”。在实现上，定义两个游标i和j，一开始均指向数组的第一个元素，让i去遍历数组的各个元素，当i遍历到的元素的值和函数的输入参数相同时，利用continue来让i指代下一个元素。当i指代的数组元素和函数的输入参数不同的时候，把数组a[j]的值赋成数组a[i]的值，同时让j++，这时，j代表的就是当前剔除特殊值后的数组元素的个数，同时i没遇到一个不需要剔除的元素的时候，都会让其去覆盖a[j]处的元素。

# 二. Remove Duplicates from sorted Array

> Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length. Do not allocate extra space for another array, you must do this in place with constant memory. For example, Given input array A = [1,1,2], your function should return length = 2, and A is now [1,2].

要求：给定一个分类好的数组，剔除掉数组中重复出现的元素，从而让每个元素最多出现一次，并且返回数组新的长度。不允许分配新的内存，上述工作必须在原数组中进行。

## 1.Solution
``` C++
#include <iostream>
using namespace std;

class Solution
{
public:
	int removeDup(int a[], int n);
};

int Solution::removeDup(int a[], int n)
{
	int i = 1, j = 0;
	for(; i < n; i++)
	{
		if(a[i] == a[j])
		{
			continue;
		}
		else
		{
			a[j+1] = a[i];
			j++;
		}
	}
	return j + 1;
}

int main()
{
	int a[6] = {1,2,2,3,3,4};
	Solution b;
	cout << "处理前数组的内容为";
	for(int i = 0; i < 6; i++)
	{
		cout << a[i] << " ";
	}
	int result = b.removeDup(a, 6);
	cout << endl << "处理后数组的长度为" << result << "数组的内容为";
	for(int j = 0; j < result; j++)
	{
		cout << a[j] << " ";
	}
}
```

## 2. Analysis
这道题和上道题非常类似，同样给定一个数组后需要两个游标i和j，分别指向数组的第1、2个元素。让i一次遍历所有元素，若a[i] == a[j]，则i自增，知道a[i] != a[j]，则将a[j+1]赋值为a[i]，之后使i和j都自增1. 一开始的时候我担心在将a[j+1]赋值成a[i]的时候会把某些数组的元素给覆盖掉，但是仔细分析其实并不会。因为如果j+1 < i，则说明中途有重复的，那就可以随便覆盖了；当中途没有重复的时候，则j+1 = i，此时a[j+1] = a[i]，赋值等于没动，因此可以放心地去弄。

# 三. Remove Duplicates from sorted Array II

> Follow up for "Remove Duplicates": What if duplicates are allowed at most twice? For example, Given sorted array A =[1,1,1,2,2,3], your function should return length = 5, and A is now [1,1,2,2,3]

要求： 和前面一道题差不多，只不过这个要求不是消灭重复的，而是消灭超过重复三个的。

## 1.Solution
``` c++
#include <iostream>
using namespace std;

class Solution
{
public:
	int removeDup(int a[], int n);
};

int Solution::removeDup(int a[], int n)
{
	int j = 0, i = 1, times = 0;
	while( i < n )
	{
		if((a[i] == a[j])&&(times == 0))
		{
			times++;
			i++;
		}
		else if((a[i] == a[j])&&(times == 1))
		{
			a[j+1] = a[i];
			i++;
			j++;
		}
		else if(a[i] != a[j])
		{
			times = 0;
			a[j+1] = a[i];
			i++;
			j++;
		}
	}
	return j + 1;
}

int main()
{
	int a[6] = {1,1,1,2,2,4};
	Solution b;
	cout << "处理前数组的内容为";
	for(int i = 0; i < 6; i++)
	{
		cout << a[i] << " ";
	}
	int result = b.removeDup(a, 6);
	cout << endl << "处理后数组的长度为" << result << "数组的内容为";
	for(int j = 0; j < result; j++)
	{
		cout << a[j] << " ";
	}
}
```

## 2. Analysis
看到这道题后，我的第一反应是按照和2类似的处理，但是需要额外地添加个判断，即在第二次发生相等的时候才会执行上一题第一次判断相等的时候的操作。因此，我加入了记录次数的变量times，并且初始化为0，当检测到有元素相等且times为0的时候，即判断这是第一次遇到相等的元素，则不采取任何操作，当判断到相等且times为1，则判断是第二次遇到了相等，执行上一题相等时候的操作。当遇到不等的情况时，采取的做法和上一题一样，但是要注意得把times变量置为0。这道题我在一开始就想到了思路，但是写的时候写了挺久，没能够善于应用第二题的结论，导致出现了好多小问题。

# A Conclusion

|             消灭排序好的重复元素的操作               |
|------------------------------------------------------|
|遇到不等的时候，让小游标的下一个元素的值等于大游标的值|
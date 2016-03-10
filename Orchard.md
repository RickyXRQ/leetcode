#*Template*

# X. Problem Name

> The content of the Problem

要求： 中文版的题目的具体要求

## 1.Solution:
```C++
C++ code here
```
## 2.Analysis:
My analysis here.

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

# 三. Plus One

> Given a non-negative number represented as an array of digits, plus one to the number. The digits are stored such that the most significant digit is at the head of the list

要求： 给出一个按位存储的非负数，给这个非负数加1。 这个数的存储形式是高位在前。

## 1.Solution:
```C++
#include <iostream>
#include <vector>
using namespace std;


class Solution
{
public:
	vector<int> plusOne(vector<int> &digits)
	{
		vector<int> res(digits.size(),0);
		int sum = 0;
		int one = 1;
		for(int i = digits.size() - 1; i >= 0; i--)
		{
			sum = one + digits[i];
			one = sum / 10;
			res[i] = sum % 10;
		}
		if(one > 0)
		{
			res.insert(res.begin(), one);
		}
		return res;
	}
};

class Solution2
{
public:
	vector<int> plus1(vector<int> digits)
	{
		vector<int> res(digits.size(),0);
		int sum = 0;
		int add = 0;
		for(int i = digits.size()-1; i >=0; i--)
		{
			if(i == digits.size() - 1)
			{
				sum = digits[i] + 1;
			}
			else
			{
				sum = add + digits[i];
			}
			add = sum / 10;
			res[i] = sum % 10;
		}
		if(add > 0)
		{
			res.insert(res.begin(),1);
		}
		return res;
	}
};

int main()
{
	vector<int> a(4,0);
	vector<int>::iterator it;
	int i = 4;
	for(it = a.begin(); it != a.end(); it++)
	{
		*it = i;
		i--;
	}
	Solution2 xu;
	vector<int> result(a.size(),0);
	result = xu.plus1(a);
	for(it = result.begin(); it != result.end(); it++)
	{
		cout << *it << endl;
	}
	Solution temp;
	vector<int> result2(a.size(),0);
	result2 = temp.plusOne(a);
	for(it = result2.begin(); it != result2.end(); it++)
	{
		cout << *it << endl;
	}
}

```
## 2.Analysis:
一开始拿到这道题我没什么思路，因为它说的按照digit来存储，所以我想到了数组。但是用数组来存储如果遇到进位的情况会比较麻烦。我就看了答案。答案是用vector来实现的。上面贴的代码中，Solution是答案的代码，Solution2是我自己写的代码，答题思路一样，无非就是让最低位加1，因为加1后可能涉及到进位，所以要把和对10取余后作为结果的对应位数，而把和除以10的结果作为进位的结果（因为都是int型）。需要注意的是，在做完后，还得看最后进位有没有，如果有的话则需要在最前面添加1，即999999作为输入参数的情况。对比我和答案，还是我太死板了，因为one这个变量就在一开始用过以后就再也不用了，因此完全没必要像我那样分情况讨论的。。。 
**这道题我觉得对于我来说比较重要的两点是：**
- 按位加法的实现思路
	按位相加后，对10取余的结果进位，除以10的结果和本位相加
- 对vector的应用

# 四. Pascal's Triangle

> Given numRows, generate the first numRows of Pascal's triangle.

For example, give numRows = 5, Return

[1]

[1,1]

[1,2,1]

[1,3,3,1]

[1,4,5,4,1]

要求： 输入一个正整数，输出类似的三角形。

```C++
#include <iostream>
#include <vector>
using namespace std;

class Solution
{
public:

	vector<vector<int>> PascalTriangle3(int n)
	{
		vector<vector<int>> result;
		result.resize(n);
		for(int i = 0; i < n; i++)
		{
			result[i].resize(i+1);
			result[i][0] = 1;
			result[i][result[i].size() - 1] = 1;
			for(int j = 1; j < result[i].size()-1; j++)
			{
				//if(i == 0 || i == 1)
				//	continue;
				result[i][j] = result[i-1][j-1] + result[i-1][j];
			}
		}
		return result;
	}
};

int main()
{
	vector<vector<int>> result;
	cout << "please cin a number" << endl;
	int num;
	cin >> num;
	result.resize(num);
	Solution a;
	result = a.PascalTriangle3(num);
	vector<vector<int>>::iterator itr1;
	vector<int>::iterator itr2;

	for(itr1 = result.begin(); itr1 != result.end(); itr1++)
	{
		cout << "[";
		for(itr2 = itr1->begin(); itr2 != itr1->end(); itr2++)
		{
			cout << (*itr2) << " ";

		}
		cout << "]" << endl;
	}
	return 1;
}

```
## 2.Analysis:
这道题观察规律方面不难，但是实话说花了我大半个晚上的时间。究其原因是我用错了vector的iterator，如果定义了vector<vector<int>>::iterator itr，貌似是不能用**itr来输出int的值的。最后也是参考了答案的思路，因为总结的规律A[m][n] = A[m-1][n-1] + A[m-1][n]，注意这儿有可能越界的地方，给的答案没法正确执行就是因为它没有注意到越界这个问题。实现起来用两层vector，然后用数组的用法来实现值的变化。因为这个数字三角每一行的第一个和最后一个数都是1，所以可以一开始就把这些1给赋值好。以后再循环赋值的时候就别管最后一个值，这样就不会有越界的危险。

# 五. Pascal's Triangle II

> Given an index k, return the kth row of the Pascal's triangle. For example, given k = 3, return [1,3,3,1]

要求： 和上一道类似，只不过是只要求输出第n行，不需要全部输出，注意，这道题要求的空间复杂度是O(n)

## 1.Solution:
``` C++
#include <iostream>
#include <vector>
using namespace std;

class Solution
{
public:

	vector<int> PascalTriangle(int n)
	{
		vector<int> result(n,0);
		int i = 1;
		while(i <= n)	//这层循环用来生成第n行，因为第n行需要从第1行开始逐渐累加，因此需要从第一行开始逐渐生成
		{
			result[0] = result[i-1] = 1;
			if(i >= 3)
			{
				int j = i-2;
				for(;j > 0;j--)		//这层循环用来做由第n-1行生成n行的叠加运算
				{
					result[j] = result[j] + result[j-1];
				}
			}
			i++;
		}
		return result;
	}
};

int main()
{
	Solution a;
	cout << "Please enter a number" << endl;
	int n;
	cin >> n;
	vector<int> result(n);
	result = a.PascalTriangle(n);
	for(vector<int>::iterator itr = result.begin(); itr != result.end(); itr++)
	{
		cout << (*itr) << " ";
	}
	return 1;
}
```
## 2.Analysis:
因为空间复杂度要求为o(n)，因此就不能用二维数组的vector，需要用一维的vector来反复更新值。如对于第5行来说，其实是vector[0] = 1; vector[1] = vector[1] + bector[0]; vector[2] = vector[2] + vector[1]; vector[3] = vector[3] + vector[2]; 但是如果我们自己简单地这样写的话，会遇到一个问题，比如第二句更新了vector[1]的值，在计算新的vector[2]的时候就不能借用上一行的vector[1]了，为了避免这个问题，我们在实现的时候应该按照上面倒序的形式来写，即vector[3] = vector[3] + vector[2]; vector[2] = vector[2] + vector[1]; vector[1] = vector[1] + bector[0];  这样的话，在对每一行进行从后到前的更新时，后面更新的值不会影响前面值的更新。

# 六. Merge Sorted Array

> Given two sorted integer arrays A and B, merge B into A as one sorted array. Node: you may assume that A has enough space(size that is greater or equal to m+n) to hold additional elements from B. The number of elements initialized in A and B are m and n respectively.

要求： 有两个排序好的数组A和B，将这两个数组合并为一个数组，并且保持从小到大的顺序。

``` C++
#include <iostream>
#include <vector>
using namespace std;

#define MAXSIZE 100

class Solution
{
public:
	void MergeArray(int a[], int an, int b[], int bn)
	{
		int i = 0, j = 0;
		while( j < bn)
		{
			if(b[j] < a[i])
			{
				//前插(把b[j]的值插到a[i]前)
				for(int temp1 = an; temp1 > i; temp1--)
				{
					a[temp1] = a[temp1 - 1];
				}
				a[i] = b[j];
				j++;
				an++;
			}
			else
			{
				if(i < an - 1)
				{
					i++;
				}
				else
				{
					//把b[j]所有的值插到a[i]后， 因为到这一步，可以认为b后面所有的值都大于a的值了
					for(int temp = 0; temp < bn - j; temp++)
					{
						a[i + 1 + temp] = b[j + temp];
					}
					break;
				}
			}
		}
	}
};

int main()
{
	Solution res;
	int a[MAXSIZE];
	for(int i = 0; i < MAXSIZE; i++)
	{
		a[i] = 0;
	}
	a[0] = 1;
	a[1] = 3;
	a[2] = 9;
	a[3] = 10;
	a[4] = 11;
	int b[3] = {5,17,23};
	int an = 5, bn = 3;
	res.MergeArray(a,an,b,bn);
	for(int j = 0; j < MAXSIZE; j++)
	{
		if(a[j] == 0)
		{
			break;
		}
		else
		{
			cout << a[j] << " ";
		}
	}
}
```
## 2.Analysis:
这道题我的思路是这样的，遍历第二个数组b，找到a中比b大的元素，如果找到，则将b前插在这个元素之前，同时让数组a的长度增加1，继续访问b的下一个元素。用这个逻辑来遍历b中的所有元素。特殊情况是b的某一个元素比a的最后一个元素都大，那么问题就好办了，直接把b中的这个元素及其后面所有的元素添加到a元素的后面。前插就是线性表的插入操作。对两个数组赋了不同的值，各种情况下都能通过。**答案用了一种很巧妙的方法：因为两个数组合并后的新数组的元素一定是m+n-1，因此就从a和b中从后往前访问，把二者的较大值赋值给a的m+n-1，然后指在m+n-1的游标减1继续操作即可**


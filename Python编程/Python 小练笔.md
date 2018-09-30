# Python 小练笔
九月二十八日
问题描述：扫雷游戏，输入m,n,number分别代表行、列、雷数，返回对应雷数的随机坐标列表。

```
#引入随机数模块和时间模块（计算效率）
import random
import time
def saolei():
    m = input("请输入行数：")
    n = input("请输入列数： ")
    number = input("请输入雷数：")
    temp = 0
    results = []
    start = time.time()
    while temp < int(number):
        mRandom = random.randint(1, int(m))
        nRandom = random.randint(1, int(n))
        results.append((mRandom, nRandom))
        #去重
        result = set(results)
        if len(result)-1 == temp:
            temp += 1
        continue
    end = time.time()
    print(result)
    print(end-start)

saolei()


运行结果：
请输入行数：10
请输入列数： 1
请输入雷数：10
{(9, 1), (7, 1), (8, 1), (6, 1), (3, 1), (2, 1), (10, 1), (5, 1), (4, 1), (1, 1)}
0.0009720325469970703
```
效率更高的思路：
默认在m*n的点阵中所有地方都有雷，每次随机到一个坐标就pop出列表，从而减少去重的过程。

九月二十九
二分法查询：
思想：
假如有一组数为3，12，24，36，55，68，75，88要查给定的值24.可设三个变量front，mid，end分别指向数据的上界，中间和下界，mid=（front+end）/2.
1.开始令front=0（指向3），end=7（指向88），则mid=3（指向36）。因为a[mid]>x，故应在前半段中查找。
2.令新的end=mid-1=2，而front=0不变，则新的mid=1。此时x>a[mid]，故确定应在后半段中查找。
3.令新的front=mid+1=2，而end=2不变，则新的mid=2，此时a[mid]=x，查找成功。
如果要查找的数不是数列中的数，例如x=25，当第三次判断时，x>a[mid]，按以上规律，令front=mid+1，即front=3，出现front>end的情况，表示查找不成功。

```
def binary(numberlist,number):
    front = 0
    end = len(numberlist) - 1
    error = "Error to search"
    while front <= end:
        middle = (front+end)//2
        if numberlist[middle] == int(number):
            return middle
        if numberlist[middle] > int(number):
            end = middle - 1
        if numberlist[middle] < int(number):
            front = middle + 1
    return error


if __name__ == "__main__":
    numberlist = [3, 12, 24, 36, 55, 68, 75, 88]
    value = binary(numberlist, 24)
    print(value)


运行结果：
2
```

九月三十日
冒泡排序：
思想：
冒泡排序算法的原理如下：
比较相邻的元素。如果第一个比第二个大，就交换他们两个。
对每一对相邻元素做同样的工作，从开始第一对到结尾的最后一对。在这一点，最后的元素应该会是最大的数。
针对所有的元素重复以上的步骤，除了最后一个。
持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。 
冒泡排序总的平均时间复杂度为O(n^2)
```
def bubble(numberlist):
    numberlength = len(numberlist)
    while numberlength > 0:
        for item in range(numberlength - 1):
            if numberlist[item] > numberlist[item + 1]:
               numberlist[item],numberlist[item+1] = numberlist[item+1],numberlist[item]
         numberlength = numberlength - 1
    return numberlist

if __name__ == "__main__":
    numberlist = [3, 4, 1, 2, 5, 8, 0]
    value = bubble(numberlist)
    print(value)
    
输出：[0, 1, 2, 3, 4, 5, 8]
```

```
def bubble_sort(nums):
    for i in range(len(nums) - 1):  # 这个循环负责设置冒泡排序进行的次数
        for j in range(len(nums) - i - 1):  # j为列表下标
            if nums[j] > nums[j + 1]:
                nums[j], nums[j + 1] = nums[j + 1], nums[j]
    return nums


print(bubble_sort([45, 32, 8, 33, 12, 22, 19, 97]))

输出结果：[8, 12, 19, 22, 32, 33, 45, 97]
```


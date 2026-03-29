# 前言
我在做 P1309 是两个 TLE，后来用归并排就 A 了，所以来整理一下所有~~偷懒~~的 STL 函数（~~其实本来就想整理的~~）

注：这些全是个人积累。
# 开始
## iota —— ABC
生成一串升序数列
::::success[用法]
```cpp
iota(开始迭代器,结束迭代器,起始数字);//[)
```
::::
::::info[示例]
```cpp
#include <numeric>
vector<int> a(10);
iota(a.begin(),a.end(),0);//a = {0,1,2,3,4,5,6,7,8,9}
```
::::
## stable_sort —— P1309
将数列分开排序（类似归并）。
::::success[用法]
```cpp
stable_sort(开始迭代器,结束迭代器,排序方式);//和 sort 差不多
```
::::
::::info[示例]
#include <algorithm>
vector<int> a({1,4,5,6,3,2});
stable_sort(a.begin(),a.end());//a = {1,2,3,4,5,6}
::::
## merge —— P1309
归并排。
::::success[用法]
```cpp
merge(begin,end,cmp)//和 sort 一样
```
::::
::::info[示例]
```cpp
#include <algorithm>
merge(a,a+n+1);
```
::::

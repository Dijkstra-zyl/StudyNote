# Problem
实现一个 Black Box，可以进行一下功能：
```text
ADD(x)：把 x 元素放进 Black Box;
GET：i 加 1，然后输出 Black Box 中第 i 小的数。
```
# Solution
我们通过观察题目中的例子，不难发现，对于所有的操作，如果当前的 Black Box 中的元素个数小于 $u_i$ 时，就不能输出，否则移动下标，在不能输出的时候，不断地加入 $a_i$。

所以这个问题可以进一步抽象成：动态维护一个序列，对于每个 `GET` 输出序列中第 $i+1$ 大的数。
## Input
处理输入很简单，代码如下：
```cpp
const int N = 2e5+10;
int m,n,a[N],u[N];
cin >> m >> n;
for(int i = 1;i <= m;i++) cin >> a[i];
for(int i = 1;i <= n;i++) cin >> u[i];
```
## Data Struture
对于这一类问题，我们可以使用 **对顶堆** 这一数据结构来解决，避免使用其他高级数据结构的繁琐。

对于对顶堆，可以看我的[这篇博客](https://www.luogu.com.cn/article/ro2sxjs4)来学习堆的相关知识。

我们用小根堆来维护前 $k$ 大的数（包括 $k$），用大根堆来维护后 $k$ 大的数（不包括 $k$），对于每次 `GET` 只需输出小根堆的堆顶元素即可，这样的时间复杂度较少。

## Solve
在下标遍历时，会执行一下步骤：
```text
如果 当前序列中的数的数量 < k（也就是 u[i]）
  则 继续往序列中加入 a[i]，进行 ADD 操作，不断遍历 a[i]，先将其加入大根堆，获得最小元素后加入小根堆
如果 当前序列中的数的数量 > k
  则 停止循环，输出小根堆的堆顶元素，也就是第 k 大的数，并且弹出
下标++
```
易得，下标 $i \in [1,n]$。
## Output
每次序列中的数的数量大于 $u_i$ 时，输出小根堆中的堆顶元素即可，记得弹出，否则 $\mathrm{TLE}$。
# Code
代码方面，小/大根堆可以使用 $\mathrm{STL}$ 中的优先队列来模拟。

**注意**：`greater<int>()` 为小根堆。
```cpp
#include <iostream>//对顶堆
#include <queue>
#include <vector>
using namespace std;
const int N = 2e5+10;
priority_queue<int,vector<int>,greater<int>> q1;
priority_queue<int,vector<int>,less<int>>    q2;
int a[N],u[N];
int main(){
	int m,n; cin >> m >> n;
	for(int i = 1;i <= m;i++) cin >> a[i];
	for(int i = 1;i <= n;i++) cin >> u[i];
    int cnt = 0;
	for(int i = 1;i <= n;i++){
		while(cnt < u[i]){//若小根堆中的数量<k
			q2.push(a[++cnt]);//先加入大根堆
			q1.push(q2.top());//加入大根堆的最小元素到小根堆
			q2.pop();//大根堆要弹出
		}
		cout << q1.top() << endl;
		q2.push(q1.top());
		q1.pop();
	}
	return 0;
}
```

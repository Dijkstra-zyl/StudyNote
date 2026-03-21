# 总结
这次比赛 AB 题能稳定 AC，而 C 题 AC*8，TLE*18，DEFG 题没看。
# A $\pi$
## Knowledge
考察浮点处理与圆的面积公式。
 
算法：$\color{red}{\sf{模拟}}$
## Problem
给定一个圆的直径 D，求圆的面积，答案相差不大于 $10^{-6}$。
## Solve
可以使用一个浮点数常量 $\texttt{PI}$ 来存储圆周率后 10 位，然后用圆的面积公式计算即可。
```cpp
#include <iostream>
#include <cstdio>
using namespace std;
const double PI = 3.1415926535
int mian(){
    int d; cin >> d;
    printf("%.10lf",PI * (d/2.0) * (d/2.0));
    return 0;
}
```
# B Deconstruct Chocolate
## Knowledge
考察二维空间的理解与题意转化。

算法：$\orange{\sf{数学}}$
## Problem
给定一个 N 行 M 列的巧克力，和 Q 行 query，格式如下：
 
```text
N M Q
query_1
query_2
 ...
query_Q
```
对于每个 query：
 
```text
1 R：输出底部 R 行的块数，并吃掉
或
2 C：输出右侧 C 列的块数，并吃掉
```
## Solve
在这里，我们只需要存储行和列即可，不用更新。
 
- 对于操作 1，底部 R 行的块数等于 $R * M$，行数减 R
- 对于操作 2，右侧 C 列的块数等于 $C * N$，列数减 C
 
```cpp
#include <iostream>
#include <cstdio>
using namespace std;
const int N = 110;
int n,m,q,ans;
int main(){
    cin >> n >> m >> q;
    ans = n * m;
    while(q--){
    		int query; cin >> query;
    		if(query == 1){//行
    			int r; cin >> r;
    			cout << m * r << endl;
    			n -= r;
    		}else{//列
    			int c; cin >> c;
    			cout << n * c << endl;
    			m -= c;
    		}
 	}
	return 0;
}
```
# C Comfortable Distance
## Knowledge
 
## Problem
给定一个长度为 N 的字符串 S 和 L、R。
 
求满足一下条件的数对对数：
- $1 \le i \le j \le N$
- $S_i = S_j$
- $L \le j-i \le R$
## Solve
### Lite
首先可以使用暴力，枚举 $i \in [1,N]$ 和 $j \in [i,N]$，再判断，注意这里的字符串是从 $1$ 开始的。
 
```cpp
#include <iostream>
#include <cstdio>
using namespace std;
const int N = 5e5+10;
int n,l,r,ans;
char s[N];
int main(){
  	ios::sync_with_stdio(0),cin.tie(0);
   	cin >> n >> l >> r;
   	for(int i = 1;i <= n;i++) cin >> s[i];
   	for(int i = 1;i <= n;i++)
   		for(int j = i;j <= n;j++)
   			if(s[i] == s[j] && l <= j-i && j-i <= r) ans++;
   	cout << ans << endl;
  	return 0;
}
```
Sample $AC \times 3$   
Other  $AC \times 5\ \ \ TLE \times 18$
### Pro
 
# D、E、F、G 题等 C 题稳定 AC 再说

# A 3,2,1,Go
## Problem
给定一个正整数 $N$，按照 $N,N-1,N-2...1$ 的顺序输出一行，用 ',' 分割。
## Solve
考察：**模拟+循环**

利用循环一次减一即可，注意 ','：

```cpp
#include <iostream>
using namespace std;
int n;
int main(){
    cin >> n;
    for(int i = n;i > 1;i--) cout << i << ",";
    cout << 1;
    return 0;
}
```
# B Split Ticketing
## Problem
给定 $N$ 个车站，以及从 $i$ 站下车上 $j$ 站的价格 $C_{i,j}$。

寻找一组 $a,b,c$，使得：
- $1 \lq a < b < c \lq N$
- $C_{a,b} + C_{b,c} < C_{a,c}$

如果有输出 'Yes'，否则输出 'No'。
## Solve
考察：**二维数组+理解能力+循环嵌套**

因为 $1 \lq N \lq 100$，所以可以考虑使用循环遍历，预计 $O(n^3)$。

可以遍历 $a \in [1,N]$，$b \in [a+1,N]$，$c \in [b+1,N]$，然后判断即可，另外注意输入：

```cpp
#include <iostream>
using namespace std;
const int N = 110;
int n,c[N][N];
int main(){
    cin >> n;
    for(int i = 1;i < n;i++) for(int j = i+1;j <= n;j++) cin >> c[i][j];
    for(int a = 1;a <= n;a++){
        for(int b = a+1;b <= n;b++)
            for(int c = b+1;c <= n;c++)
                if(c[a][b] + c[b][c] < c[a][c]) return cout << "Yes",0;
    cout << "No";
    return 0;
}
```
# C Puddles
## Problem
有一个 $H$ 行 $W$ 列的网格，对于第 $(i,j)$ 上的情况由 $S_{i,j}$ 表示。
- $S_{i,j}$ 为 '#'，表示涂上黑色
- $S_{i,j}$ 为 '.'，表示涂上白色

求四周被黑色包围的块的数量。
## Solve
考察：**连通性问题（搜索）**

- Step1:读入一个网格
- Step2:处理网格边缘上的块，所以要用一个 $dfs$ 来讲他整个替换成其他的东西，比如 $@$，因为边上的不应该计算，并没有全部被包围
- Step3:使用连通块的代码进行解决并计算个数
- Step4:输出个数

```cpp
#include <iostream>
using namespace std;
const int N = 1e3+10;
int n,m,cnt;
char s[N][N];
int d[][2] = {{0,1},{1,0},{-1,0},{0,-1}};//偏移量
int vis[N][N],vis2[N][N];//两个判断是否走过的
void dfs(int x,int y){//用于连通块
	if(x < 1 || x > n || y < 1 || y > m || vis[x][y] || s[x][y] == '@' || s[x][y] == '#') return;//是否越界
	vis[x][y] = 1;//标记
	for(int i = 0;i < 4;i++) dfs(x+d[i][0],y+d[i][1]);//遍历邻居
}
void ddfs(int x,int y){//用于更换边上的
	if(x < 1 || x > n || y < 1 || y > m || vis2[x][y] || s[x][y] == '#') return;//越界 碰到#说明这一块到头了 所以才标记成其他的
	s[x][y] = '@';
	vis2[x][y] = 1;
	for(int i = 0;i < 4;i++) ddfs(x+d[i][0],y+d[i][1]);
}
int main(){
	cin >> n >> m;
	for(int i = 1;i <= n;i++) 
		for(int j = 1;j <= m;j++) cin >> s[i][j];
	for(int i = 1;i <= m;i++){//将网格四周的块替换
		if(s[1][i] != '#') ddfs(1,i);
		if(s[n][i] != '#') ddfs(n,i);
	}
	for(int i = 1;i <= n;i++){
		if(s[i][1] != '#') ddfs(i,1);
		if(s[i][m] != '#') ddfs(i,m);
	}
	
	//cout << endl;
	//for(int i = 1;i <= n;i++,puts("")) 
	//	for(int j = 1;j <= m;j++) cout << s[i][j];
	//return 0;
	
	for(int i = 1;i <= n;i++){//连通块代码
		for(int j = 1;j <= m;j++){
			if(!vis[i][j] && s[i][j] == '.'){
				dfs(i,j);
				cnt++;
			}
		}
	}
	cout << cnt;
	return 0;
}
```
# 剩下的不会了，研究题解ing...

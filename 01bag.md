# dp
//01bag
#include<iostream>
#include<cstring>
using namespace std;

const int N = 1010;
int n,m;
int v[N], w[N];
int res=0;
//第几个物品，剩余容积，总价值
//int dfs(int x,int spV,int sumW) {
//	if (x > n) return res;
//	if (sumW > res) res = sumW;
//	else if (spV < v[x]) {//体积不够只能不选
//		return dfs(x + 1, spV, sumW);
//	}
//	else {//体积够，可以选或者不选
//		return max(dfs(x + 1, spV - v[x], sumW + w[x]), dfs(x + 1, spV, sumW));
//	}
//}

//记忆化搜索O(2^n)->O(n*V)
//int mem[N][N];
//int dfs(int x, int spV) {
//	if (mem[x][spV]) return mem[x][spV];
//	int sum = 0;
//	if (x > n) sum= 0;
//	else if (spV < v[x]) {
//		sum= dfs(x + 1, spV);
//	}
//	else if (spV >= v[x]) {
//		sum= max(dfs(x + 1, spV), dfs(x + 1, spV - v[x]) + w[x]);
//	}
//	mem[x][spV] = sum;
//	return sum;
//}
int f[N][N] = { 0 };
int main() {
	scanf_s("%d %d", &n, &m);
	for (int i = 1; i <= n; i++) {
		scanf_s("%d %d", &v[i], &w[i]);
	}
	//递推
	
	for (int i = n; i >= 1; i--) {
		for (int j = 0; j <= m; j++) {
			//f[i][j]表示从第i个物品到结尾物品，选取的体积不超过j的最大价值
			if (j < v[i]) {//不够装
				f[i][j] = f[i + 1][j];
			}
			else if (j >= v[i]) {//够装
				f[i][j] = max(f[i + 1][j], f[i + 1][j - v[i]] + w[i]);
			}
		}
	}
	cout << f[1][m];
	return 0;
}
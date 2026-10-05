## 语法

如果临时变量不赋值默认不是0

return 1有的时候判处runtime error

计算比例的时候不要用除法 用乘法

字符串转换为数字的方法stoi stoll

st count

写dp的时候一定考虑数据的范围，如果超过要高精度或者long long 

LLONG_MAX = 9223372036854775807

动态规划 01背包

一个物品只能选择一次

因此要倒叙选择，因为从后往前不影响 不会选择多次

dp[j]就是j元最多有多少方案

回溯

有组合型回溯，要把组合里的东西一次分配在数组里面，因此选用for

还有选不选的回溯，

```
intb[500][500] = {-1};
```

只有第一个元素是 -1。

vector pop_back

## 常见结论

10 ≈ 2^3.322

## 二进制

输出二进制语法 bitset

```cpp
#include <iostream>
#include <bitset>
using namespace std;

int main() {
    int x = 10;
    cout << bitset<8>(x) << endl;
}

处理二进制字符串
for(auto ch: s){
      for(int i = 7; i >= 0; i--){
          cur += '0' + ((ch >> i) & 1);
      }
  }
```

## 质数分解

```cpp
for(int i = 2; i * i <= b; i++){
                if((b % i) == 0){
                    cur.push_back(i);
                    while((b % i) == 0){
                        b = b / i;
                    }
                }
            }
            if(b > 1) cur.push_back(b);
            a.push_back(cur);
```

只需要分解到sqrt 最后把自己加上

## Floyd最短路径

时间复杂度n^3

要求无环，图中再任意两个点中间找另外一个点，是否更短

必须要更新的顺序就是k i j

第 k 轮结束后：
dis[i][j] 表示只允许经过 1~k 号节点作为中间点时，
i 到 j 的最短距离。

```cpp
for(int i = 1; i <= n; i++){
        for(int j = 1; j <= n; j++){
            dis[i][j] = (i == j ? 0 : INF);
        }
    }

   for(int k = 1; k <= n; k++){
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= n; j++){
            
                dis[i][j] = min(dis[i][j], dis[i][k] + dis[k][j]);
            }
        }
    }

```

## 常见错误

常规分支有if 特殊分支没有

越界访问的时候边界条件注意｜ &

注意根节点判断是否为空

## 最小栈

最小栈和优先队列，

最小栈可以记录大小的顺序，数据结构是一个栈，维护最大到最小的index的顺序，

优先队列自动排成最大的

## 回溯

常见错误一 尝试去更改子节点的状态每一层都只需要更改自己的状态，没有必要更改

常见的就是判断，更改本层的状态，dfs 回复状态

## 子串

如何判断两个子串相同的组成就是用一个128大小的数组 然后和一个need记录字符的种类，

## 最小子数组和

动态规划：如果之前的数组和拖累现在的值，就另起炉灶

线段树：建立一个状态，然后用pushup返回分治的结果


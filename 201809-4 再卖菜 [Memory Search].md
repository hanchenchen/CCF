# 201809-4 再卖菜 [Memory Search]

```c++
#include<bits/stdc++.h>
#include<iostream>
#include<vector>
#include<queue>
#include<math.h>
using namespace std;
const int maxN=300+5;
int after[maxN],before[maxN],n;
bool vis[maxN][maxN*3][maxN*3];
void dfs(int d,int x,int y){
    if(vis[d][x][y])return;
    vis[d][x][y]=true;
    if(d==n){
        if((x+y)/2==after[n]){
            for(int i=1;i<=n;i++){
                if(i!=1)cout<<" ";
                cout<<before[i];
            }
            cout<<endl;
            exit(0);
        }
        return ;
    }
    for(int i=0;i<3;i++){
        before[d+1]=3*after[d]-x-y+i;
        if(before[d+1]<1)continue;
        dfs(d+1,y,before[d+1]);
    }
}
int main(){
    fill(vis[0][0],vis[0][0]+maxN*maxN*maxN*9,false);
    cin>>n;
    for(int i=1;i<=n;i++)cin>>after[i];
    for(int i=1;i<2*after[1];i++){
        before[1]=i;before[2]=2*after[1]-i;
        dfs(2,before[1],before[2]);
        before[1]=i;before[2]=2*after[1]-i+1;
        dfs(2,before[1],before[2]);
    }
    
    return 0;
}
/*
 8
 2 2 1 3 4 9 10 13
 */
```

##### Reference

[ccf再卖菜](https://blog.csdn.net/imotolove/article/details/82777819)
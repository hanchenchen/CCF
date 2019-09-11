# 201812-4 数据中心 [kruscal] [graph]

```c++
#include<iostream>
#include<vector>
#include<algorithm>
#include<bits/stdc++.h>

using namespace std;
const int maxN=1e5+5;
const int maxM=1e5+5;
int n,m,root,father[maxN];
struct V{
    int v,u,t;
}vertex[maxM];
int getf(int x){
    int y=x;
    while(x!=father[x])x=father[x];
    while(y!=x){
        int z=y;
        y=father[y];
        father[z]=x;
    }
    return x;
}
int main(){
    ios::sync_with_stdio(false);
    cin>>n>>m>>root;
    for(int i=0;i<m;i++){
        cin>>vertex[i].v>>vertex[i].u>>vertex[i].t;
    }
    for(int i=1;i<=n;i++){
        father[i]=i;
    }
    sort(vertex,vertex+m,[](V a,V b){
        return a.t<b.t;
    });
    int ans=0;
    for(int i=0;i<m;i++){
        int l=getf(vertex[i].v);
        int r=getf(vertex[i].u);
        if(l!=r){
            father[max(l,r)]=min(l,r);
            ans=max(ans,vertex[i].t);
        }
    }
    printf("%d\n",ans);
    return 0;
}
/*
 4 5 1
 1 2 3
 1 3 4
 1 4 5
 2 3 8
 3 4 2
 
 */
```


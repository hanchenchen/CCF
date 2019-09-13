# 201609-4 交通规划 [dijkstra]

```c++
//#include<bits/stdc++.h>
#include<iostream>
#include<vector>
using namespace std;
const int maxN=1e4+1;
struct road{
    int b,w;
};
vector<road> r[maxN];
int n,m,ans=0,cost[maxN]={0},vis[maxN]={0},dis[maxN];
void dijkstra(){
    fill(dis,dis+maxN,INT_MAX);
    dis[1]=0;
    //cost[1]=0;
    for(int i=0;i<n;i++){
        int mini=INT_MAX,pos=-1;
        for(int j=1;j<=n;j++){
            if(!vis[j]&&mini>dis[j]){
                mini=dis[j];
                pos=j;
            }
        }
        if(pos==-1)return;
        vis[pos]=1;
        ans+=cost[pos];
        for(int j=0;j<r[pos].size();j++){
            //cout<<r[pos][j].w<<endl;
            if(vis[r[pos][j].v])continue;
            if(dis[r[pos][j].v]>dis[pos]+r[pos][j].w){
                dis[r[pos][j].v]=dis[pos]+r[pos][j].w;
                cost[r[pos][j].v]=r[pos][j].w;
            }else if(dis[r[pos][j].v]==dis[pos]+r[pos][j].w){
                if(cost[r[pos][j].v]>r[pos][j].w){
                    cost[r[pos][j].v]=r[pos][j].w;
                }
            }
        }
    }
}
int main(){
    cin>>n>>m;
    int x,y,z;
    //fill(weight[0],weight[0]+maxN*maxN,INT_MAX);
    for(int i=0;i<m;i++){
        cin>>x>>y>>z;
        //weight[x][y]=weight[y][x]=z;
        r[x].push_back({y,z});
        r[y].push_back({x,z});
    }
    dijkstra();
    cout<<ans<<endl;
    return 0;
}
/*
4 5
1 2 4
1 3 5
2 3 2
2 4 3
3 4 2
*/
```


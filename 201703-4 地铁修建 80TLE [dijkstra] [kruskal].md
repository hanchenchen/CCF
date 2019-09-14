# 201703-4 地铁修建 80TLE [dijkstra] [kruskal]

```c++
//#include<bits/stdc++.h>
#include<iostream>
#include<vector>
#include<unordered_map>
#include<math.h>
using namespace std;
const int maxN=1e5+5;
struct edge{
    int e,val;
};
vector<edge> g[maxN];
int n,m,dis[maxN]={0},vis[maxN]={0};
void dijkstra(){
    fill(dis,dis+n+1,INT_MAX);
    dis[1]=0;
    for(int i=1;i<=n;i++){
        int pos=-1,mini=INT_MAX;
        for(int j=1;j<=n;j++){
            if(!vis[j]&&mini>dis[j]){
                pos=j;
                mini=dis[j];
            }
        }
        if(pos==-1||pos==n)return;
        vis[pos]=1;
        for(int j=0;j<g[pos].size();j++){
            if(dis[g[pos][j].e]>max(g[pos][j].val,dis[pos])){
                dis[g[pos][j].e]=max(g[pos][j].val,dis[pos]);
            }
        }
    }
}
int main(){
    cin>>n>>m;
    int a,b,c;
    while(m--){
        cin>>a>>b>>c;
        g[a].push_back({b,c});
        g[b].push_back({a,c});
    }
    dijkstra();
    cout<<dis[n]<<endl;
    return 0;
    
}

```


# 201612-3 权限查询 [string] [map]

```c++
//#include<bits/stdc++.h>
#include<iostream>
#include<unordered_map>
using namespace std;
const int maxN=1e2+5;
int p,r,u,q,char_null=100;
unordered_map<string,int> p_level;
unordered_map<string,unordered_map<string,int>> role,user;
int main(){
    string s;
    scanf("%d\n",&p);
    for(int i=0;i<p;i++){
        getline(cin,s);
        if(isdigit(*s.rbegin())){
            p_level[s.substr(0,(int)s.size()-2)]=*s.rbegin();
        }else{
            p_level[s]=char_null;
        }
    }
    int n;string rname;
    scanf("%d\n",&r);
    for(int i=0;i<r;i++){
        cin>>rname;
        scanf("%d ",&n);
        for(int j=0;j<n;j++){
            cin>>s;
            if(isdigit(*s.rbegin())){
                if(*s.rbegin()>=role[rname][s.substr(0,(int)s.size()-2)])
                    role[rname][s.substr(0,(int)s.size()-2)]=*s.rbegin();
            }else{
                role[rname][s]=char_null;
            }
        }
    }
    scanf("%d\n",&u);
    for(int i=0;i<u;i++){
        cin>>rname;
        scanf("%d ",&n);
        for(int j=0;j<n;j++){
            cin>>s;
            for(auto it:role[s]){
                if(it.second>=user[rname][it.first])
                    user[rname][it.first]=it.second;
            }
        }
    }
    /*for(auto it:user){
        cout<<it.first<<endl;
        for(auto j:it.second){
            cout<<j.first<<" "<<j.second-'0'<<" "<<endl;
        }
    }*/
    scanf("%d\n",&q);
    for(int i=0;i<q;i++){
        cin>>rname;
        cin>>s;
        int x=char_null;
        if(isdigit(*s.rbegin())){
            x=*s.rbegin();
            s=s.substr(0,(int)s.size()-2);
        }
        if(user.find(rname)==user.end()){
            printf("false\n");
        }else if(user[rname].find(s)==user[rname].end()){
            printf("false\n");
        }else if(x==char_null){
            if(user[rname][s]==char_null){
                printf("true\n");
            }else{
                printf("%d\n",user[rname][s]-'0');
            }
        }else if(x!=char_null){
            if(user[rname][s]<x){
                printf("false\n");
            }else{
                printf("true\n");
            }
        }
    }
    return 0;
}
/*
 3
 crm:2
 git:3
 game
 4
 hr 1 crm:2
 it 3 crm:1 git:1 game
 dev 2 git:3 game
 qa 1 git:2
 3
 alice 1 hr
 bob 2 it qa
 charlie 1 dev
 9
 alice game
 alice crm:2
 alice git:0
 bob git
 bob poweroff
 charlie game
 charlie crm
 charlie git:3
 malice game
 */

```


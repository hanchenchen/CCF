# -201812-3 CIDR合并 90 TLE[string]

```c++
//#include<bits/stdc++.h>
#include<iostream>
#include<vector>
#include<queue>
#include<math.h>
using namespace std;
typedef long long ll;
//const int maxN=1e5+5;
struct p{
    int len=0;
    ll h=0,x=0;
};
vector<p> ip;
void func(string &s,int i){
    int dot=(int)count(s.begin(),s.end(),'.');
    int sub=(int)s.find('/');
    if(sub==string::npos){
        ip[i].len=8*(dot+1);
    }else{
        ip[i].len=stoi(s.substr(sub+1));
    }
    for(int j=0,k;j<s.size();j++){
        k=(int)s.find('.',j);
        if(k==string::npos)k=(int)s.size();
        ip[i].x<<=8;
        ip[i].x+=stoi(s.substr(j,k-j));
        //cout<<ip[i].x<<endl;
        j=k;
    }
    dot=3-dot;
    for(int j=0;j<dot;j++){ip[i].x<<=8;}
    int r=32-ip[i].len;
    ip[i].h=ip[i].x;
    ip[i].h+=(1<<r)-1;
    //cout<<r<<" "<<ip[i].x<<" "<<ip[i].h<<endl;
}
int main(){
    int n;cin>>n;
    string s;
    vector<p> (n).swap(ip);
    for(int i=0;i<n;i++){
        cin>>s;
        func(s,i);
    }
    sort(ip.begin(),ip.end(),[](const p &a,const p &b){
        //if(a.len!=b.len)return a.len<b.len;
        if(a.x!=b.x)return a.x<b.x;
        return a.h>b.h;
    });
    for(int i=0;i<ip.size()-1;i++){
        if(ip[i+1].x>=ip[i].x&&ip[i+1].h<=ip[i].h){
            ip.erase(ip.begin()+i+1);
            i--;
        }
    }
    for(int i=0;i<ip.size()-1;i++){
        if(ip[i].len==ip[i+1].len){
            int l=ip[i].len;
            if((ip[i+1].x>>(32-l+1))==(ip[i].x>>(32-l+1))&&
               ((ip[i+1].x>>(32-l))&1)^((ip[i].x>>(32-l))&1)){
                ip[i].h=ip[i+1].h;
                ip.erase(ip.begin()+i+1);
                ip[i].len--;
                /*ip[i].x>>=(32-ip[i].len);
                 ip[i].x<<=(32-ip[i].len);*/
                i--;
            }
        }
    }
    /*
    sort(ip.begin(),ip.end(),[](const p &a,const p &b){
        if(a.h!=b.h)return a.h>b.h;
        if(a.x!=b.x)return a.x<b.x;
        return a.len<b.len;
    });
    for(int i=0;i<ip.size()-1;i++){
        if(ip[i+1].x>=ip[i].x&&ip[i+1].h<=ip[i].h){
            ip.erase(ip.begin()+i+1);
            i--;
        }
    }
     */
    /*
    sort(ip.begin(),ip.end(),[](const p &a,const p &b){
        if(a.x!=b.x)return a.x<b.x;
        if(a.h!=b.h)return a.h>b.h;
        return a.len<b.len;
    });*/
    
    for(int i=0;i<ip.size();i++){
        vector<ll> ans(4);
        ll x=ip[i].x;
        x>>=(32-ip[i].len);
        x<<=(32-ip[i].len);
        for(int i=0;i<4;i++){
            ans[3-i]=x&((1<<8)-1);
            x>>=8;
        }
        for(int i=0;i<4;i++){
            printf("%lld",ans[i]);
            if(i!=3)printf(".");
        }
        printf("/%d\n",ip[i].len);
    }
    return 0;
}
/*
 4
 2/8
 3/8
 2/7
 0/7
 
 0.0.0.0/6
 */
```

##### `char []` 90 TLE

```c++
//#include<bits/stdc++.h>
#include<iostream>
#include<vector>
#include<queue>
#include<math.h>
using namespace std;
typedef long long ll;
//const int maxN=1e5+5;
struct p{
    int len=0;
    ll h=0,x=0;
};
vector<p> ip;
void func(char s[],int i){
    int dot=(int)count(s,s+strlen(s),'.');
    int sub=(int)strlen(s)-1;
    while(sub>0&&s[sub]!='/')sub--;
    if(sub==0){
        ip[i].len=8*(dot+1);
        s[(int)strlen(s)-1]='\0';
    }else{
        ip[i].len=atoi(s+sub+1);
        s[sub]='\0';
    }
    for(int i=dot;i<3;i++){
        strcat(s,".0");
        //cout<<s<<endl;
    }
    ll a,b,c,d;
    sscanf(s,"%lld.%lld.%lld.%lld",&a,&b,&c,&d);
    ip[i].x=(a<<24)+(b<<16)+(c<<8)+d;
    int r=32-ip[i].len;
    ip[i].h=ip[i].x;
    ip[i].h+=(1<<r)-1;
    //cout<<r<<" "<<ip[i].x<<" "<<ip[i].h<<endl;
}
int main(){
    int n;cin>>n;
    getchar();
    char s[30];
    vector<p> (n).swap(ip);
    for(int i=0;i<n;i++){
        fgets(s,30,stdin);
        func(s,i);
    }
    sort(ip.begin(),ip.end(),[](const p &a,const p &b){
        //if(a.len!=b.len)return a.len<b.len;
        if(a.x!=b.x)return a.x<b.x;
        return a.h>b.h;
    });
    for(int i=0;i<ip.size()-1;i++){
        if(ip[i+1].x>=ip[i].x&&ip[i+1].h<=ip[i].h){
            ip.erase(ip.begin()+i+1);
            i--;
        }
    }
    for(int i=0;i<ip.size()-1;i++){
        if(ip[i].len==ip[i+1].len){
            int l=ip[i].len;
            if((ip[i+1].x>>(32-l+1))==(ip[i].x>>(32-l+1))&&
               ((ip[i+1].x>>(32-l))&1)^((ip[i].x>>(32-l))&1)){
                ip[i].h=ip[i+1].h;
                ip.erase(ip.begin()+i+1);
                ip[i].len--;
                /*ip[i].x>>=(32-ip[i].len);
                 ip[i].x<<=(32-ip[i].len);*/
                i--;
            }
        }
    }
    /*
    sort(ip.begin(),ip.end(),[](const p &a,const p &b){
        if(a.h!=b.h)return a.h>b.h;
        if(a.x!=b.x)return a.x<b.x;
        return a.len<b.len;
    });
    for(int i=0;i<ip.size()-1;i++){
        if(ip[i+1].x>=ip[i].x&&ip[i+1].h<=ip[i].h){
            ip.erase(ip.begin()+i+1);
            i--;
        }
    }
     */
    /*
    sort(ip.begin(),ip.end(),[](const p &a,const p &b){
        if(a.x!=b.x)return a.x<b.x;
        if(a.h!=b.h)return a.h>b.h;
        return a.len<b.len;
    });*/
    
    for(int i=0;i<ip.size();i++){
        ll x=ip[i].x;
        //x>>=(32-ip[i].len);
        //x<<=(32-ip[i].len);
        for(int i=3;i>=0;i--){
            printf("%lld",(x>>8*i)&((1<<8)-1));
            if(i!=0)printf(".");
        }
        printf("/%d\n",ip[i].len);
    }
    return 0;
}
/*
 4
 2/8
 3/8
 2/7
 0/7
 
 0.0.0.0/6
 */


```


# 201803-3 URL映射 90WA[string] 

1. `/<int>/`和`/<int>`是不一样的

#### string

```c++
//#include<bits/stdc++.h>
#include<iostream>
#include<vector>
#include<unordered_map>
#include<math.h>
using namespace std;
const int maxN=100+5;
unordered_map<char,bool> if_legal;
struct URL{
    string id;
    vector<string> path;
}url[maxN];
bool ifLegal(string &s){
    for(int i=0;i<s.size();i++){
        if(isalnum(s[i])||if_legal[s[i]])continue;
        return false;
    }
    return true;
}
int if_rear_sub=1;
bool ifEqual(vector<string> &role,vector<string> &v,vector<string> &ans){
    int i,j;
    for(i=0,j=0;i<role.size()&&j<v.size();i++){
        if(role[i]=="<str>"){
            ans.push_back(v[j]);
            j++;
        }else if(role[i]=="<int>"){
            for(auto c:v[j])if(!isdigit(c))return false;
            ans.push_back(to_string(stoi(v[j])));
            j++;
        }else if(role[i]=="<path>"){
            string s;
            for(;j<v.size();j++){
                s=s+v[j];
                if(j!=(int)v.size()-1)s=s+'/';
            }
            if(if_rear_sub)s=s+'/';
            ans.push_back(s);
            return true;
        }else{
            if(role[i]!=v[j])return false;
            j++;
        }
    }
    return (i==role.size()&&j==v.size());
}
int main(){
    if_legal['-']=if_legal['_']=if_legal['.']=true;
    int n,m;cin>>n>>m;
    string s;
    for(int i=0;i<n;i++){
        cin>>s>>url[i].id;
        for(int j=1,k;j<s.size();j++){
            k=(int)s.find('/',j);
            if(k==string::npos)k=(int)s.size();
            url[i].path.push_back(s.substr(j,k-j));
            j=k;
        }
    }
    string mid;
    for(int i=0;i<m;i++){
        bool flag=true;if_rear_sub=1;
        cin>>s;
        vector<string> v,ans;
        for(int j=1,k;j<s.size();j++){
            k=(int)s.find('/',j);
            if(k==string::npos){
                k=(int)s.size();
                if_rear_sub=0;
            }
            mid=s.substr(j,k-j);
            //cout<<"?"<<mid<<endl;
            if(!ifLegal(mid)){
                flag=false;
                break;
            }//cout<<"!"<<mid<<endl;
            v.push_back(mid);
            j=k;
        }
        if(!flag){
            cout<<"404"<<endl;
            continue;
        }
        for(int j=0;j<n;j++){
            ans.clear();
            if(ifEqual(url[j].path,v,ans)){
                flag=false;
                cout<<url[j].id;
                for(auto it:ans){
                    cout<<" "<<it;
                }
                cout<<endl;
                break;
            }
        }
        if(flag)cout<<"404"<<endl;
       
    }
    
}
/*
 5 4
 /articles/02003/ special_case_2003
 /articles/<int>/ year_archive
 /articles/<int>/<int>/ month_archive
 /articles/<int>/<int>/<str>/ article_detail
 /static/<path> static_serve
 /articles/2003/
 /articles/1985/09/aloha/
 /articles/hello/
 /static/js/jquery.js
 */


```

```
 5 4
 /articles/2003/ special_case_2003
 /articles/<int>/ year_archive
 /articles/<int>/<int>/ month_archive
 /articles/<int>/<int>/<str>/ article_detail
 /static/<path> static_serve
 /articles/2004/
 /articles/1985/09/aloha/
 /articles/hello/
 /static/js/jquery.js 
```


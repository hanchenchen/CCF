```
//#include<bits/stdc++.h>
#include<iostream>
#include <regex>
#include<unordered_map>
using namespace std;
string remove(string s){
    string ans;
    for(int i=0;i<s.size();i++){
        if(s[i]!='/')ans+=s[i];
        else if(i>0&&s[i-1]=='/'&&s[i]=='/')ans+=s[i];
    }
    return ans;
}
unordered_map<string,string> mp;
string s,mid;
void func(int start,string pre){
    string key,value;
    int i=start;
    int j=(int)s.find(':',start);
    while(s[i]!='"')i++;
    while(s[j]!='"')j--;
    key=remove(s.substr(i+1,j-i-1));
    i=j+1;
    int k=(int)s.find('}',i);
    j=(int)s.find(',',i);
    if(k!=string::npos&&k<j){
        
    }
    if(j==string::npos)return;
    func(j+1,pre);
}
int main(){
    int n,m;
    cin>>n>>m;
    getchar();
    while(n--){
        getline(cin,mid);
        s+=mid;
    }
    for(int i=0,j;i<json.size();i++){
        j=(int)json.find('"',i);
        i=j+1;
        while(json[j-1]=='/')j=(int)json.find('"',j+1);
        key=remove(json.substr(i,j-i));
        i=j+1;
        j=(int)json.find(':',i)+1;
        while(json[j]==' ')j++;
        if(json[j]=='{'){
            if(root=="")root=key;
            else root=root+"."+key;
            i=j+1;
        }else{
            i=j+1;
            j=(int)json.find('"',i);
            i=j+1;
            while(json[j-1]=='/')j=(int)json.find('"',j+1);
            value=remove(json.substr(i,j-i));
            mp[root+key]=value;
        }
    }
    for(auto it:mp){
        cout<<it.first<<"  "<<it.second<<endl;
    }
}

```


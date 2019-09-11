# **201903-3** 损坏的RAID5 100/100 [string] [fgets]

1. `fgets(disk[x],maxK,stdin);` ：70->100

2. 不用储存异或的结果也能AC

   ```c++
   #include<iostream>
   #include<string.h>
   #include<algorithm>
   #include<climits>
   #include<vector>
   #include<map>
   using namespace std;
   const int maxN=1e3+5;
   const int maxK=1e5+5;
   char disk[maxN][maxK],nor_ans[258][258];
   char toChar(int x){
       if(x<10)return (char)(x+'0');
       return (char)(x+'A'-10);
   }
   int toInt(char x){
       if(x<='9'&&x>='0')return (int)(x-'0');
       return (int)(x-'A'+10);
   }
   int main(){
       for(int i=0;i<16;i++){
           for(int j=0;j<16;j++){
               nor_ans[toChar(i)][toChar(j)]=toChar(i^j);
           }
       }
       int n,s,l,x,y,len=0;
       scanf("%d %d %d",&n,&s,&l);
       for(int i=0;i<l;i++){
           scanf("%d ",&x);
           //scanf("%s",disk[x]);
           fgets(disk[x],maxK,stdin);
           len=(int)strlen(disk[x]);
       }
       int m;cin>>m;
       for(int h=0;h<m;h++){
           scanf("%d",&x);
           int row=x/(s*(n-1));
           int p=n-1-row%n;
           int diskNum=(1+p+x%(s*(n-1))/s)%n;
           //printf("%d %d\n",row,diskNum);
           y=8*(row*s+x%s);
           //cout<<y<<endl;
           
           if(y+8<=strlen(disk[diskNum])){
               for(int i=y;i<y+8;i++){
                   printf("%c",disk[diskNum][i]);
               }printf("\n");
           }else if(y+8>len||n-l>1){
               printf("-\n");
           }else{
               char ans[10]={"00000000"};
               for(int i=0;i<n;i++){
                   if(i==diskNum)continue;
                   for(int j=y;j<y+8;j++){
                       ans[j-y]=nor_ans[ans[j-y]][disk[i][j]];
                   }
               }
               for(int i=0;i<8;i++){
                   printf("%c",ans[i]);
               }printf("\n");
           }
       }
       return 0;
   }
   
   
   /*
    3 2 2
    0 000102030405060710111213141516172021222324252627
    1 A0A1A2A3A4A5A6A7B0B1B2B3B4B5B6B7C0C1C2C3C4C5C6C7
    2
    2
    5
    
    A0A1A2A3
    A0A0A0A0
    
   2 1 2
   0 99910293849596971811121314151617282122232425262718
   1 99910283949596071811121314151617292122232425262720
   2
   0
   1
    */
   ```

3. 1




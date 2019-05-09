# 8-Puzzle-Solver
Mata Kuliah Kecerdasan Buatan

### # CPP Files

### 1. Algoritma DLS
```sh
#include<bits/stdc++.h>
using namespace std;

unordered_map<string,string>parents;

int getInvCount(int puzzle[]){
    int counter = 0;
    for(int i = 0; i < 8; i++){
        for(int j = i+1; j < 9; j++){
            if(puzzle[i] && puzzle[j] && puzzle[i] > puzzle[j]){
                counter++;
            }
        }
    }
    return counter;
}

bool isSolveable(int puzzle[3][3]){
    int invCount = getInvCount((int *)puzzle);

    return(invCount%2==0);
}



void DLS8P(string s, string p, int d){
    if(parents.count(s) || d > 35){
        return;
    }
    parents[s]=p;
    if(s=="123456780"){
        stack<string>batang;
        string tmp;
        tmp=s;
        while(tmp!=""){
            batang.push(tmp);
            tmp=parents[tmp];
        }

        while (!batang.empty()){
            tmp = batang.top();
            batang.pop();
            for(int i = 0; i < 9; i++){
                cout << tmp[i];
                if(i%3==2) cout << endl;
            } cout << endl;
        }
        exit(0);
    }else{
        int index;
        for(int i = 0; i < 9; i++){
            if(s[i]=='0') index=i;
        }
        string tmp = s;
        if(index!=2 && index!=5 && index!=8){

            swap(tmp[index],tmp[index+1]);
            DLS8P(tmp,s,d+1);
            swap(tmp[index],tmp[index+1]);
        }
        if(index!=0 && index!=3 && index!=6){

            swap(tmp[index],tmp[index-1]);
            DLS8P(tmp,s,d+1);
            swap(tmp[index],tmp[index-1]);
        }
        if(index!=0 && index!=1 && index!=2){

            swap(tmp[index],tmp[index-3]);
            DLS8P(tmp,s,d+1);
            swap(tmp[index],tmp[index-3]);
        }
        if(index!=6 && index!=7 && index!=8){

            swap(tmp[index],tmp[index+3]);
            DLS8P(tmp,s,d+1);
            swap(tmp[index],tmp[index+3]);
        }

    }
}

int main(){
    string s, a, b, c;
    cin >> a;
    cin >> b;
    cin >> c;
    s=a+b+c;

    int arr[3][3];
    int counter=0;
    for(int i = 0; i < 3; i++){
        for (int j = 0; j < 3; j++){
            arr[i][j] = s[counter]-'0';
            counter++;
        }
    }

    cout << endl;
    if(isSolveable(arr))
    DLS8P(s,"",0);
    else{
        cout << "Puzzle is not solveable" << endl;
    }
}
```

### 2. Algoritma DFS
```sh
#include <bits/stdc++.h>
using namespace std;
#pragma comment(linker, "/STACK:6000000")
unordered_map<string,string>parents;

int getInvCount(int puzzle[]){
    int counter = 0;
    for(int i = 0; i < 8; i++){
        for(int j = i+1; j < 9; j++){
            if(puzzle[i] && puzzle[j] && puzzle[i] > puzzle[j]){
                counter++;
            }
        }
    }
    return counter;
}

bool isSolveable(int puzzle[3][3]){
    int invCount = getInvCount((int *)puzzle);

    return(invCount%2==0);
}


void DFS8P(const string& s, const string& p){

    string b = s;
    if(parents.count(b)){
        //cout << b<<endl;
        return;
    }
    if(s=="123456780"){
        //cout << "oiiii" << endl;
        parents[s]=p;
        stack<string>batang;
        string x;
        x=s;
        while (x!=""){
            batang.push(x);
            x=parents[x];
        }

        while (!batang.empty()){
            string y = batang.top();
            batang.pop();
            for(int i = 0; i < 9; i++){
                cout << y[i];
                if(i%3==2){
                    cout << endl;
                }
            }
            cout << endl;
        }

    exit(0);
    }else{

        parents[s]=p;
        int index;

        for(int i = 0; i < 9; i++){
            if (s[i]=='0'){
                index = i;
            }
        }
        //cout << index << endl;
        string x=s;
        if(index != 2 && index != 5 && index != 8){
            swap(x[index], x[index+1]);
            DFS8P(x,s);
            swap(x[index], x[index+1]);
        }
        //cout << s << endl;

        if(index != 0 && index !=3 && index != 6){
            swap(x[index], x[index-1]);
            DFS8P(x,s);
            swap(x[index], x[index-1]);
        }

        if(index != 0 && index !=1 && index != 2){
            swap(x[index], x[index-3]);
            DFS8P(x,s);
            swap(x[index], x[index-3]);
        }

        if(index != 6 && index !=7 && index != 8){
            swap(x[index], x[index+3]);
            DFS8P(x,s);
            swap(x[index], x[index+3]);
        }
    }
}

int main(){
    string s, a, b, c;
    cin >> a;
    cin >> b;
    cin >> c;
    s=a+b+c;
    int counter=0;
    int arr[3][3];
    for(int i = 0; i < 3; i++){
        for (int j = 0; j < 3; j++){
            arr[i][j] = s[counter]-'0';
            counter++;
        }
    }

    if(isSolveable(arr))
    DFS8P(s,"");
    else{
        cout << "Puzzle is not solveable" << endl;
    }

}
```

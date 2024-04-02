# hhhhhyx加的乱七八糟的

## 关闭同步流

```cpp
ios::sync_with_stdio(false);
cin.tie(0);
cout.tie(0);
```

## 快读快写

+ 快读1

```cpp
inline int read(){
    int x=0,f=1;
    char c=getchar();
    while(c<'0'||c>'9') f=(c=='-')?-1:1,c=getchar();
    while(c>='0'&&c<='9') x=x*10+c-'0',c=getchar();
    return x*f;
}
```

+ 快读2

```cpp
template<typename T>
inline void r(T &x) {
    x = 0;
    int ch = getchar();
    while (ch < 48 || ch > 57)
        ch = getchar();
    while (ch >= 48 && ch <= 57)
        x = (x << 1) + (x << 3) + ch - 48, ch = getchar();
    return;
}
```

+ 快读3（调大S加速，同时占用空间增加）

```cpp
namespace INPUT_SPACE{
	const int S=(1<<20)+5;char B[S],*H,*T;inline int gc() { if(H==T) T=(H=B)+fread(B,1,S,stdin);return (H==T)?EOF:*H++; }
	inline unsigned int inn() { unsigned int x,ch;while((ch=gc())<'0'||ch>'9');x=ch^'0';while((ch=gc())>='0'&&ch<='9') x=x*10+(ch^'0');return x; }
}using INPUT_SPACE::inn;
```

+ __int128读写

```cpp
void read(__int128 &x){
	// read a __int128 variable
	char c; bool f = 0;
	while(((c = getchar()) < '0' || c > '9') && c != '-');
	if(c == '-'){f = 1; c = getchar();}
	x = c - '0';
	while((c = getchar()) >= '0' && c <= '9')x = x * 10 + c - '0';
	if(f) x = -x;
}
void write(__int128 x){
	// print a __int128 variable
	if(x < 0){putchar('-'); x = -x;}
	if(x > 9)write(x / 10);
	putchar(x % 10 + '0');
}
```

## 高精度

+ 高精度加法

```cpp
// C = A + B, A >= 0, B >= 0
vector<int> add(vector<int> &A, vector<int> &B){
    if (A.size() < B.size()) return add(B, A);
    vector<int> C;
    int t = 0;
    for (int i = 0; i < A.size(); i ++ ){
        t += A[i];
        if (i < B.size()) t += B[i];
        C.push_back(t % 10);
        t /= 10;
    }
    if (t) C.push_back(t);
    return C;
}
```

+ 高精度减法

```cpp
// C = A - B, 满足A >= B, A >= 0, B >= 0
vector<int> sub(vector<int> &A, vector<int> &B){
    vector<int> C;
    for (int i = 0, t = 0; i < A.size(); i ++ ){
        t = A[i] - t;
        if (i < B.size()) t -= B[i];
        C.push_back((t + 10) % 10);
        if (t < 0) t = 1;
        else t = 0;
    }
    while (C.size() > 1 && C.back() == 0) C.pop_back();
    return C;
}
```

## 快速幂

```cpp
int qpow(int a,int b,int mod){
	int ans=1;
	while(b){
		if(b&1) ans=ans*a%mod;
		a=a*a%mod;
		b>>=1;
	}
	return ans;
}
```
# 常用STL

## vector

+ 排序去重

```cpp
vector<int> alls;
sort(alls.begin(), alls.end());
alls.erase(unique(alls.begin(), alls.end()), alls.end());
```
## string

+ substr

```cpp
string s = "abcdef";
cout << s.substr(2) << endl; // cdef
cout << s.substr(2, 2) << endl; // cd
cout << s.substr(3, -1) << endl; // def
cout << s.substr(3, string::npos) << endl; // def
```

+ replace

```cpp
string s = "abcdef";
s.replace(3, 2, "123456");
cout << s << endl; // abc123456f
s = "abcdef";
s.replace(3, 2, "123456", 2, 3); // abc345f
cout << s << endl;
s = "abcdef";
s.replace(3, 1, 5, '#');
cout << s << endl; // abc#####ef
```

+ find

```cpp
string s = "abcdef";
cout << s.find('c') << endl; // 输出为 2
// 从下标3开始找第一个字符'c'
// 此时，由于查找不到，如返回的是stirng::npos
// 这个输出值是size_t的最大值，对不同系统输出不一
cout << s.find('c', 3) << endl; 
// 但在判断是否找到可以用这种方式
if (s.find('3', 3) == string::npos) {
    cout << "not find!!!" << endl;
}
cout << s.find("bc") << endl; // 输出为 1
cout << s.find("ef", 1) << endl; // 输出为 4
```

+ stoi（字符串转指定进制）

```cpp
string s="123456789";
int s=stoi(s,0,10);
```

## 优先队列priority_queue

empty()如果队列为空返回真

pop()删除堆顶元素

push()加入一个元素

size()返回元素个数

top()返回队顶元素

在默认的优先队列中，优先级高的先出队。在默认的int型中先出队的为较大的数

```cpp
priority_queue<int> q1;//大的先出队
priority_queue<int,vector<int>,greater<int> >q2;//小的先出队
```

自定义比较函数：

```cpp
struct cmp{
    bool operator ()(int x,int y){
        return x>y;//x小的优先级高
        //也可以写成其他方式，如p[x]>p[y]
    }
};
riority_queue<int,vector<int>,cmp>q2;
```

```cpp
struct node{
    int x,y;
    friend bool operator < (node a,node b){
        retrun a.y>b.y;//y小的优先级高
    }
};
priority_queue<node> q;
//在该结构体中，x为值，y为优先级
//通过重载运算符来比较元素中的优先级
//最好不要同时重载"<"和">"，可能会发生编译c错误
```

## set和multiset

set和multiset用法一样，就是multiset允许重复元素

元素放入容器时，会按照一定的排序法则自动排序，默认是按照 less<> 排序规则来排序。

不能修改容器里面的元素值，只能插入和删除。

自定义 int 排序函数：（默认的是从小到大的，下面这个从大到小）

```cpp
struct classcomp{
    bool operator () (const int& lhs,const int& rhs){
        return lhs>rhs;
    }
};
multiset<int,classcomp> mset;
```

上面这样就定义成了从大到小排列了。

结构体自定义排序函数：

（定义 set 或者 multiset 的时候定义了排序函数，定义迭代器时一样带上排序函数）

```cpp
struct node{
    int x,y;
};
struct classcomp{//先按x从小到大，相同则按y从大到小
    bool operator () (const node &a,const node &b){
        if(a.x!=b.x) return a.x<b.x;
        else return a.y>b.y;
    }
};
multiset<int,classcomp> mset;
multiset<int,classcomp>::iterator it;
```

```cpp
//主要函数
//begin() 返回指向第一个元素的迭代器
//clear() 清除所有元素
//count() 返回某个值元素的个数
//empty() 如果集合为空，返回true
//end() 返回指向最后一个元素的迭代器
//erase() 删除集合中的元素（参数是一个元素值或者迭代器）
//find() 返回一个指向被查找到元素的迭代器
//insert() 向集合中插入元素
//size() 集合中元素的数目
//lower_bound() 返回指向大于或等于某值的第一个元素的迭代器
//upper_bound() 返回大于某个值元素的迭代器
//equal_range() 返回集合中与给定值相等的上下限的两个迭代器
//对于multiset删除操作之间会把所有这个值的都删掉，删除一个要用迭代器
```

## unordered_set

除了无序外和set基本相同 没有lower_bound()和upper_bound()
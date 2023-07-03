---
title: 「研究生考试」机试笔记
date: 2021-03-26 17:41:20
tags: 研究生考试
highlight_shrink: true

---

## 机试真题

#### 数组翻转

- 从`(0, 0)`开始旋转：
  - 顺时针翻转90°    等价于  `[i, j] --> [j, n-1-i]`
  - 逆时针翻转 90°   等价于  `[i, j] --> [n-1-j, i]`

- 从 `(x, y)` 开始旋转
  - 顺时针翻转90°    等价于  `[i, j] --> [x-y+j, x+y+n-1-i]`
  - 逆时针翻转 90°   等价于  `[i, j] --> [x+y+n-1-j, y-x+i]`

### 字符串处理

> `#include <cctype>`

![image-20230512](https://cdn.jsdelivr.net/gh/SnowOnVolcano/imagebed/202305120045491.png)



## 基础知识

### struct

> **结构体**。

```
// 重载
struct fruit {
	int price;
	friend bool operator < (fruit f1, fruit f2) {
		return f1.price < f2.price;
	}
};
```

### 随机数

```c++
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main() {
	srand((unsigned)time(NULL));
	rand(); // rand()的范围是 [0, RAND_MAX]
	rand()%(b-a+1) + a; //生成[a,b]内的随机数
	1.0*rand()/RAND_MAX; //生成[0,1]之内的浮点数

}
```



------



## C++标准模板库

### vector

> 动态数组。

```c++
// 头文件
#include <vector>
using namespace std;

// 定义
vector<typrname> vi;
vector<vector<typename> > name; 
vector<typename> Arrayname[size];

// 访问
vi.begin() //首元素地址 
vi.end() //尾元素地址的下一个地址 
vector<typename>::iterator it; //迭代器
vi[i] 或 *(it+i) //访问元素 
for(it=st.begin();it != st.end(); it++) printf("% ", *it); //遍历访问
for(i=0; i < vi.size(); i++) printf("% ", *(it+i)); //遍历访问

// 常用函数
vi.push_back(x) //在vector数组的末尾添加元素x
vi.pop_back() //删除vector数组的末尾元素
vi.insert(it, x) //在vector的迭代器it处插入元素x
    
vi.erase(it) //删除it处的单个元素
vi.erase(first, last) //删除迭代器[first, last)内的所有元素
vi.clear() //清空vector中所有元素
vi.size() //获取vector数组中的元素个数
```

### set

> **集合**。① 内部自动有序（递增）；② 不含重复元素。

```c++
// 头文件
#include <set>
using namespace std;

// 定义
set<typename> st; //与vector相同

// 访问
set<typename>::iterator it; //迭代器
st.begin() //首元素地址
st.end() //尾元素地址的下一个地址 
// 不支持 st[i] 或 *(it+i) 访问方式
for(it=st.begin();it != st.end(); it++) printf("% ", *it); //遍历访问

// 常用函数
st.insert(x) //将x插入set容器，自动递增排序和去重
st.find(value) //寻找值value，返回其迭代器
st.erase(value) //删除值为value的元素
    
st.erase(it) 
st.erase(first, last) 
st.clear() 
st.size() 
```

### string

> **字符串**。

```c++
// 头文件
#include <string>
using namesapce std;

// 定义
string str;
string str = ""; //初始化

// 读入读出
#include <iostream>
cin >> str;
cout << str;
printf("%s", str.c_str()); //使用printf

// 访问
string::iterator it;
str[i] 或 *(it+i) //访问元素

// 常用函数
str3 = str1 + str2 //加法 - 字符串拼接
> >= <= < == != //比较 - 按字典序进行比较
str.insert(pos, string) //在pos号位置插入string
str.insert(it, it2, it3) //将字符串[it2, it3)插入到it的位置上
str.substr(pos, length) //获取从pos号位开始、长度为length的子串
string::npos = -1 = 4294967295 //find函数失败的返回值
str.find(str2) //str2是str的子串时，返回str2第一次出现的位置号；否则返回string::npos
str.find(str2, pos) //从pos号位开始查找
str.replace(pos, length, str2) //把str从pos号位开始、长度为length的子串替换为str2
str.replace(it1, it2, str2) //把str的迭代器[it1, it2)范围的子串替换为str2
str.erase(pos, length) //删除从pos号位、长度为length的子串
    
str.erase(it) 
str.erase(first, last) 
str.clear()
str.length() 或 str.size()
```

### map

> **映射**。①`(key, value)`：可以将任何基本类型`key`映射到任何基本类型`value`（包括STL容器）；②`key`是唯一的；③内部自动有序（键递增）。[详细参考地址。](https://www.cnblogs.com/fnlingnzb-learner/p/5833051.html)

```c++
// 头文件
#include <map>
using namespace std;

// 定义
map<typename1, typename2> mp; //typename1是键key，typename2是值value

// 访问
map[key] //访问 key对应的value
map<typename1, typename2>::iterator it;
it->first //访问当前映射的键
it->second //访问当前映射的值

// 常用函数
mp.find(key) //获取键为key的映射的迭代器，如果未找到，返回map.end()

mp.erase(it) 
mp.erase(first, last) 
mp.clear() 
mp.size() 
```

### queue

> **队列**。①先进先出。

```c++
// 头文件
#include <queue>
using namespace std; 

// 定义
queue<typename> q;

// 访问
q.front() //队首元素
q.back() //队尾元素

// 常用函数
q.push(x) //将x入队
q.pop() //令队尾元素出队
q.empty() //检测queue是否为空，返回true为空，返回false为非空

q.size()
```

### priority_queue

> **优先队列**。①底层使用“堆”实现，队首为队列中优先级最高的那个元素。

```c++
// 头文件
#include <queue>
using namespace std;

// 定义
priority_queue<typename> q; //typename可以是任意基本数据类型或容器

// 访问
q.top() //获取队首元素

// 常用函数
q.push(x) //将元素x入队
q.pop() //将队首元素出队
q.empty() 
q.size()

// 优先级设置
// 基础数据类型
priority_queue<int, vector<int>, less<int> > q; //less<int>表示数字越大的优先级越高
priority_queue<int, vector<int>, greater<int> > q; //greater<int>表示数字越小的优先级越高
priority_queue<double, vector<double>, less<int> > q;
priority_queue<char, vector<char>, less<int> > q;
// 结构体
struct fruit {
	int price;
	friend bool operator < (const fruit &f1, const fruit &f2) {
		return f1.price < f2.price;
	}
}; //方法一：重载小于号
struct fruit {
	int price;
};
struct cmp {
	bool operator () (const fruit &f1, const fruit &f2) {
		return f1.price < f2.price;
	}
};
priority_queue<fruit, vector<fruit>, cmp> q; //方法二：使用结构体外的函数
```

### stack

> **栈**。①先进后出。

```c++
// 头文件
#include <stack>
using namespace std;

// 定义
stack<typename> s;

// 访问
s.top() //访问栈顶元素

// 常用函数
s.push() //将x入栈
s.pop() //将栈顶元素出栈
s.empty()
s.size()
```

### pair

> **对**。

```c++
// 头文件
#include <utility> //使用#include<map>时会自动添加<utility>头文件
using namespace std;

// 定义
pair<typename1, typename2> p;

// 初始化
pair.first = ; pair.second = ; //方法一
p = make_pair( , ); //方法二

// 常用函数
> >= <= < == != //比较 - 先以first大小为标准，当first相等时才去判断second大小
```

### algorithm

> **常见函数工具**。

```c++
// 头文件
#include <algorithm>
using namespace std;

// 常用函数
max(x, y) //最大值
min(x, y) //最小值
abs(x) //绝对值，x必须为整数型（浮点数使用math.h下的fabs(x)）

swap(x, y) //交换x和y的值

reverse(it1, it2) //将数组指针或容器迭代器在[it1, it2)范围内的元素进行反转

fill(it1, it2, value) //把数组或容器中[it1, it2)范围内的元素赋值为value

sort(首元素地址, 尾元素地址的下一个地址, 比较函数（非必填）) //排序
sort(it1, it2) //默认为递增顺序
// 如果需要对序列进行排序，那么序列中的元素一定要具有可比性
// 基本数据类型数组的排序
int a[] = {3, 1, 2}
bool cmp(int a, int b) {return a>b;}
sort(a, a+3, cmp); //示例
// 结构体数组的排序
struct node { int x, y; }ssd[10];
bool cmp(node a, node b) {return a.x > b.x}
sort(ssd, ssd+10, cmp); //示例
// 容器数组的排序
// STL中，只有 vector， string， deque 是可以使用 sort 的
string str[3] = “a, bb, ccc”;
bool cmp(string str1, string str2) {str1.length() > str2.length()}
sort(str, str+3, cmp); //示例1
bool cmp(int a, int b) {return a>b;}
sort(vector.begin(), vector.end(), cmp); //示例2

lower_bound(first, last, value) //在[first, last)范围内寻找第一个值大于等于value的元素的位置，返回指针或迭代器
upper_bound(first, last, value) //在[first, last)范围内寻找第一个值大于value的元素的位置，返回指针或迭代器
// 上面两个函数只能用于有序数组或容器中

next_permutation(it1, it2) //给出一个序列在全排列中的下一个序列
```



------



## 数学问题

### 最大公约数

```c++
int gcd(int a, int b) {
	if (b==0) return a;
	else return gcd(b, a%b);
}
```

### 最小公倍数

```c++
int lcm(int a, int b) {
	return a / gcd(a,b) * b;
}
```

### 素数

> 素数的判断：对于数 `n`，只需要判断 `2~sqrt(n)`是否整除 `n` 即可；
>
> `1~n`素数表的求解：从小到大枚举所有数，对每一个素数，筛去它的所有倍数。

```c++
const int MAXN = 10;
bool isPrime[MAXN];

int main() {

    int n;
    cin >> n;
	
	// 素数的判断
	int t = (int)sqrt(1.0 * n);
    bool isP = true;
    for (int i=2; i<=t; i++) {
        if (n % i == 0) {
            isP = false;
            break;
        }
    }
    cout << isP << endl;
	
	// 素数表的求解
    fill(isPrime, isPrime+n+1, true);
    vector<int> store;
    for (int i=2; i<=n; i++) {
        if (isPrime[i]) {
            store.push_back(i);
            for (int j=i+i; j<=n; j+=i) {
                isPrime[j] = false;
            }
        }
    }
    for (int i=0; i<store.size(); i++) {
        cout << store[i] << " ";
    }
    return 0;
}
```

### 质因子分解

```c++
const int MAXN = 0x3ffffff;

int isprime[MAXN];

void get_prime(int n, vector<int> &store) {

    fill(isprime, isprime+n+1, true); // 易错点，记得加1

    for (int i=2; i<=n; i++) {
        if (isprime[i]) {
            store.push_back(i);
            for (int j=i+i; j<=n; j+=i) {
                isprime[j] = false;
            }
        }
    }
}

struct node{
    int num;
    int time;
    node() {}
    node(int _n, int _t) {
        num = _n;
        time = _t;
    }
};

int main() {
    int in;
    scanf("%d", &in);
    int re_in = in;

    if (in == 1) {
        cout << "1=1" <<endl;
        return 0;
    }

    int n = (int)sqrt(1.0 * in);

    vector<int> store;
    get_prime(n, store); // 计算质数

    vector<node> results;

    for (int i=0; i<store.size(); i++) { // 求质因子
        int gcc = 0;
        int t = store[i];
        if (in%t==0) {
            while (in%t==0) {
                in = in/t;
                gcc++;
            }
            results.push_back(node(t, gcc));
        }
        if (in==1) break;
    }
    if (in!=1) {
        results.push_back(node(in, 1));
    }

    return 0;
}

```

### 大整数 加减乘除

> 一个思路：先实现无符号的运算，再实现有符号的运算；
>
> 几个技巧：使用struct存储，数组逆序存储，符号单独存储，设置length字段。

```c++
struct bign {
    int num[10000]; //存储数字(绝对值)
    bool sign; //true:负; false:正
    int length; //长度

    bign() {
        memset(num, 0, sizeof(num));
        sign = false;
        length = 0;
    }
};

void delete_zero(bign &a) {
    int i=a.length-1;
    for (; i>0 && a.num[i]==0; i--);
    a.length = i + 1;
}

void init(bign &a, char input[], int n) {

    if (input[0]=='-'){ a.sign = true; }

    for (int i=a.sign?1:0; i<n; i++) {
        a.num[n-1-i] = input[i] - '0';
    }

    a.length = a.sign ? n-1 : n;
    delete_zero(a);
}

string bign2string(bign a) {
    static char re[10000];
    int index = 0;
    if (a.sign) re[index++] = '-';
    for (int i=a.length-1; i>=0; i--) {
        re[index++] = '0' + a.num[i];
    }
    if (a.length == 1 && a.num[0]==0) re[index++] = 0;
    re[index] = '\0';
    return re;
}

// if a>b return 1; else if a<b return -1; else if a==b return 0;
int compare_unsign(bign a, bign b) {
    int flag;
    if (a.length != b.length) {
        flag = (a.length > b.length) ? 1 : -1;
    }
    else {
        flag = 0;
        for (int i=a.length-1; i>=0; i--) {
            if (a.num[i] < b.num[i]) {
                flag = -1;
                break;
            }
            else if (a.num[i] > b.num[i]) {
                flag = 1;
                break;
            }
        }
    }
    return flag;
}


bign add_unsign(bign a, bign b) {
    bign c;
    int loop = max(a.length, b.length);
    int up = 0; //进位
    for (int i=0; i<loop; i++) {
        int t = a.num[i] + b.num[i] + up;
        c.num[i] = t % 10;
        up = t / 10;
    }
    if (up) { c.num[loop] = up; c.length = loop + 1;}
    else { c.length = loop; }
    return c;
}

bign sub_unsign(bign a, bign b) {
    bign c;
    bign ta = a;
    bign tb = b;
    if (compare_unsign(ta, tb)<0) {
        c.sign = true;
        swap(ta, tb);
    }
    for (int i=0; i<ta.length; i++) {
        if (ta.num[i] < tb.num[i]) {
            ta.num[i+1]--;
            ta.num[i] += 10;
        }
        c.num[i] = ta.num[i] - tb.num[i];
    }
    c.length = ta.length;
    delete_zero(c);
    return c;
}


bign mult_unsign(bign a, int b) {
    bign c;
    b = abs(b);
    int up = 0;
    int i=0;
    for (; i<a.length; i++) {
        int t = a.num[i] * b + up;
        c.num[i] = t % 10;
        up = t / 10;
    }
    while (up!=0) {
        c.num[i++] = up % 10;
        up = up / 10;
    }
    c.length = i;
    return c;
}

bign div_unsign(bign a, int b, int &r) {
    bign c;
    b = abs(b);
    r = 0;
    for (int i=a.length-1; i>=0; i--) {
        r = r*10 + a.num[i];
        if (r >= b) {
            c.num[i] = r / b;
            r = r % b;
        }
    }
    c.length = a.length;
    delete_zero(c);
    return c;
}


int compare_sign(bign a, bign b) {
    if (a.sign ^ b.sign) {
        return a.sign ? -1 : 1;
    }
    else {
        int flag = compare_unsign(a, b);
        return a.sign ? (0-flag) : flag;
    }
}

bign add_sign(bign a, bign b) {
    bign c;
    if (a.sign ^ b.sign) {
        c = sub_unsign(a, b);
    }
    else {
        c = add_unsign(a, b);
    }
    if (a.sign) c.sign = !c.sign;

    cout << bign2string(a) << " + " << bign2string(b) << " = " << bign2string(c) << endl;

    return c;
}

bign sub_sign(bign a, bign b) {
    bign c;

    if (a.sign ^ b.sign) {
        c = add_unsign(a, b);
    }
    else {
        c = sub_unsign(a, b);
    }
    if (a.sign) c.sign = !c.sign;

    cout << bign2string(a) << " - " << bign2string(b) << " = " << bign2string(c) << endl;

    return c;
}

bign mult_sign(bign a, int b) {
    bign c;
    c = mult_unsign(a, b);
    if (a.sign ^ (b<0)) {
        c.sign = true;
    }

    cout << bign2string(a) << " * " << b << " = " << bign2string(c) << endl;

    return c;
}

bign div_sign(bign a, int b, int& r) {
    bign c;

    c = div_unsign(a, b, r);

    if (a.sign ^ (b<0)) {
        c.sign = true;
        r = -r;
    }

    cout << bign2string(a) << " / " << b << " = " << bign2string(c)  << "  r=" << r <<endl;

    return c;
}


int main() {
    char ina[10000], inb[10000];
    while (scanf("%s%s", ina, inb) != EOF) {
        bign a, b;
        init(a, ina, strlen(ina));
        init(b, inb, strlen(inb));
//        cout << compare_sign(a, b) << endl;
//        add_sign(a, b);
//        sub_sign(a, b);
        int b2; sscanf(inb, "%d", &b2);
//        mult_sign(a, b2);
        int r;
        div_sign(a, b2, r);

    }

    return 0;
}
```



------



## 数据结构

### 链表（动态）

```c++
#include <cstdio>
#include <cstdlib>
#include <iostream>
#include <string>
#include <stack>
#include <vector>
#include <string.h>
#include <queue>

using namespace std;


struct node {
    // 数据域
    int data;
    // 指针域
    node* next;
};

node* creat_linklist(int data[], int length) {
    node* head = new node;
    head->data = length;
    head->next = NULL;
    node* pre = head;
    for (int i=0; i<length; i++) {
        node* p = new node;
        p->data = data[i];
        p->next = NULL;
        pre->next = p;
        pre = p;
    }
    return head;
}

node* search_linklist(node* head, int target) {
    node* p = head;
    while ((p=p->next)!=NULL) {
        if (p->data == target) {
            return p;
        }
    }
    return NULL;
}

void insert_linklist(node* head, int pos, int target) {
    node* p = head;
    for(int i=0; i<pos-1; p=p->next, i++);
    node* t= new node;
    t->data = target;
    t->next = p->next;
    p->next = t;
    head->data = head->data + 1;
}

void delete_linklist(node* head, int pos) {
    node* p = head;
    for(int i=0; i<pos-1; p=p->next, i++);
    node* pnext = p->next;
    p->next = p->next->next;
    delete(pnext);
    head->data = head->data - 1;
}


int main() {
    int a[] = {1, 2, 3, 4, 5, 6};

    node* h = creat_linklist(a, 6);
    node* s = search_linklist(h, 4);
    cout << s->data << endl;
    insert_linklist(h, 3, 0);
    for (node* p=h->next; p->next!=NULL; cout << p->data << " ", p=p->next);
    cout << endl;
    delete_linklist(h, 3);
    for (node* p=h->next; p->next!=NULL; cout << p->data << " ", p=p->next);
    cout << endl;
}
```

### 链表（静态）

```c++
struct Node {
    // 数据域
    typename data;
    // 指针域
    int next; 
}node[size];
```

### 二叉树

```c++
//存储结构
struct node {
    int data;
    node* lchild;
    node* rchild;
};

int PRE[] = {1, 2, 4, 8, 5, 9, 3, 6, 10, 11, 7, 12};
int IN[] = {8, 4, 2, 9, 5, 1, 10, 6, 11, 3, 7, 12};
int POST[] = {8, 4, 9, 5, 2, 10, 11, 6, 12, 7, 3, 1};
int LAYER[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12};

//查询
void search_tree(node* root, int target, node* &store) {
    if (root == NULL) {
        return;
    }
    else if (root->data == target) {
        store = root;
        return;
    }

    search_tree(root->lchild, target, store);
    search_tree(root->rchild, target, store);
}

//先序遍历
void pre_order_traversal(node* root) {
    if (root == NULL) {
        return;
    }
    printf("%3d ", root->data);
    pre_order_traversal(root->lchild);
    pre_order_traversal(root->rchild);
}

//中序遍历
void in_order_traversal(node* root) {
    if (root == NULL) {
        return;
    }
    in_order_traversal(root->lchild);
    printf("%3d ", root->data);
    in_order_traversal(root->rchild);
}

//后序遍历
void post_order_traversal(node* root) {
    if (root == NULL) {
        return;
    }
    post_order_traversal(root->lchild);
    post_order_traversal(root->rchild);
    printf("%3d ", root->data);
}

//层次遍历
void layer_order_traversal(node* root) {
    queue<node*> nodes;
    nodes.push(root);
    while(!nodes.empty()) {
        node* t = nodes.front();
        nodes.pop();
        if (t == NULL) {
            continue;
        }
        else {
            printf("%3d ", t->data);
            nodes.push(t->lchild);
            nodes.push(t->rchild);
        }
    }
}

//恢复二叉树：先序遍历+中序遍历
node* rebuild_pre_in(int Lpre, int Rpre, int Lin, int Rin) {
    if (Lpre>Rpre || Lin>Rin) {
        return NULL;
    }
    node* root = new node;
    root->data = PRE[Lpre];
    for (int i=Lin; i<=Rin; i++) {
        if (IN[i] == PRE[Lpre]) {
            root->lchild = rebuild_pre_in(Lpre+1, Lpre+i-Lin, Lin, i-1);
            root->rchild = rebuild_pre_in(Lpre+1+i-Lin, Rpre, i+1, Rin);
            break;
        }
    }
    return root;
}

//恢复二叉树：后序遍历+中序遍历
node* rebuild_post_in(int Lpost, int Rpost, int Lin, int Rin) {
    if (Lpost>Rpost || Lin>Rin) {
        return NULL;
    }
    node* root = new node;
    root->data = POST[Rpost];
    for (int i=Lin; i<=Rin; i++) {
        if (IN[i]==POST[Rpost]) {
            root->lchild = rebuild_post_in(Lpost, Lpost+i-Lin-1, Lin, i-1);
            root->rchild = rebuild_post_in(Lpost+i-Lin, Rpost-1, i+1, Rin);
            break;
        }
    }
    return root;
}

//恢复二叉树：层次遍历+中序遍历
node* rebuild_layer_in(vector<int> SeqLayer, int Lin, int Rin) {
    if (SeqLayer.empty() || Lin>Rin) {
        return NULL;
    }
    node* root = new node;
    root->data = SeqLayer[0];
    int flag = Lin;
    for (; flag<=Rin; flag++) {
        if (IN[flag]==SeqLayer[0]) {
            break;
        }
    }
    vector<int> LSeqLayer;
    vector<int> RSeqLayer;
    for (vector<int>::iterator it=SeqLayer.begin()+1; it!=SeqLayer.end(); it++) {
        bool isLeft = false;
        for (int j=Lin; j<flag; j++) {
            if ((*it)==IN[j]) {
                LSeqLayer.push_back((*it));
                isLeft = true;
                break;
            }
        }
        if (isLeft) {
            continue;
        }
        for (int j=flag+1; j<=Rin; j++) {
            if ((*it)==IN[j]) {
                RSeqLayer.push_back((*it));
                break;
            }
        }
    }
    root->lchild = rebuild_layer_in(LSeqLayer, Lin, flag-1);
    root->rchild = rebuild_layer_in(RSeqLayer, flag+1, Rin);
    return root;
}

int main() {
//    node* root = rebuild_pre_in(0, 11, 0, 11);
//    node* root = rebuild_post_in(0, 11, 0, 11);
    vector<int> seq;
    for (int i=0; i<12; seq.push_back(LAYER[i]), i++);
    node* root = rebuild_layer_in(seq, 0, 11);

    pre_order_traversal(root);  printf("\n");
    in_order_traversal(root);   printf("\n");
    post_order_traversal(root); printf("\n");
    layer_order_traversal(root);printf("\n");

    return 0;
}
```

### 二叉查找树 BST

```c++
struct node {
    int data;
    node* lchild;
    node* rchild;
};

void insert_BST(node* &root, int data) {
    if (root == NULL) {
        root = new node;
        root->data = data;
        root->lchild = root->rchild = NULL;
    }
    else if (root->data > data) {
        insert_BST(root->lchild, data);
    }
    else {
        insert_BST(root->rchild, data);
    }
}

node* create_BST(int input[], int n) {
    node* root = NULL;
    for (int i=0; i<n; insert_BST(root, input[i]), ++i);
    return root;
}

node* find_max_BST(node* root) {
    for(; root->rchild!=NULL; root=root->rchild);
    return root;
}

node* find_min_BST(node* root) {
    for(; root->lchild!=NULL; root=root->lchild);
    return root;
}

void delete_BST(node* &root, int target) {
    if (root == NULL) return;

    if (root->data > target) {
        delete_BST(root->lchild, target);
    }
    else if (root->data < target) {
        delete_BST(root->rchild, target);
    }
    else {
        if (root->lchild==NULL && root->rchild==NULL) {
            root = NULL;
        }
        else if (root->lchild!=NULL) {
            node* t = find_max_BST(root->lchild);
            root->data = t->data;
            delete_BST(root->lchild, t->data);
        }
        else {
            node* t = find_min_BST(root->rchild);
            root->data = t->data;
            delete_BST(root->rchild, t->data);
        }
    }
}

void in_order_traversal(node* root) {
    if (root==NULL) return;

    in_order_traversal(root->lchild);
    printf("%d ", root->data);
    in_order_traversal(root->rchild);
}


int main() {
    int seq[] = {2, 1, 4, 3, 7, 6, 5};
    node* root = create_BST(seq, 7);
    in_order_traversal(root); printf("\n");
    delete_BST(root, 5);
    in_order_traversal(root); printf("\n");
    return 0;
}
```

### 平衡二叉树 AVL

```

```

### 堆

```c++

```

### 图 - 单源最短路径算法 - Dijkstra算法

> 循环至多n次：选择距离起始点最近的、未被访问的点 ----> 更新该点所连接的点的最短路径
>
> 要求途中所有边的权重**非负**

```c++
const int MAXV = 0x1ff;
const int INF = 0x3fffffff;

// 邻接矩阵实现
void dijkstra_M(int start, int n, int Graph[MAXV][MAXV], bool Visited[], int Distance[], int Pre[]) {
    // 初始化
    fill(Distance, Distance+n, INF);
    fill(Visited, Visited+n, false);
    for (int i=0; i<n; Pre[i]=i, i++);

    // 设置起点
    Distance[start] = 0;

    for (int i=0; i<n; i++) {
        // 未被访问 && 距离起点最近 的点u
        int u = -1, minD = INF;
        for (int j=0; j<n; j++) {
            if (!Visited[j] && Distance[j]<minD) {
                u = j;
                minD = Distance[j];
            }
        }

        if (u==-1) break; //遍历结束
        else Visited[u] = true;

        // 未被访问 && 与点u相连 && 经点u可优化路径
        for (int v=0; v<n; v++) {
            if (!Visited[v] && Graph[u][v]!=INF && Graph[u][v]+Distance[u]<Distance[v]) {
                Distance[v] = Graph[u][v] + Distance[u];
                Pre[v] = u;
            }
        }
    }
}

struct Edge {
    int vertex;
    int weight;
    Edge(){}
    Edge(int _v, int _w) { vertex = _v; weight = _w;  }
};
// 邻接表实现
void dijkstra_L(int start, int n, vector<Edge> Graph[], bool Visited[], int Distance[], int Pre[]) {

    fill(Visited, Visited+n, false);
    fill(Distance, Distance+n, INF);
    for (int i=0; i<n; Pre[i]=i, i++);

    Distance[start] = 0;

    for (int i=0; i<n; i++) {

        int u = -1, minD = INF;
        for (int j=0; j<n; j++) {
            if (!Visited[j] && Distance[j]<minD) {
                u = j;
                minD = Distance[j];
            }
        }

        if (u==-1) break;
        else Visited[u] = true;

        for (int j=0; j<Graph[u].size(); j++) {
            Edge te = Graph[u][j];
            if (!Visited[te.vertex] && Distance[u] + te.weight < Distance[te.vertex]) {
                Distance[te.vertex] = Distance[u] + te.weight;
                Pre[te.vertex] = u;
            }
        }
    }
}


void DFS(int now, int start, int pre[]) {
    printf("%d ", now);
    if (now == start) return;
    DFS(pre[now], start, pre);
}

int main() {
    int n;
    scanf("%d", &n);

    int gm[MAXV][MAXV];
    fill(gm[0], gm[0]+MAXV*MAXV, INF);

    vector<Edge> gl[MAXV];

    int v1, v2, w;
    while (scanf("%d%d%d", &v1, &v2, &w) != EOF) {
        gm[v1][v2] = w;
        gl[v1].push_back(Edge(v2, w));
    }

    int dis[MAXV], pre[MAXV];
    bool vis[MAXV];
    int start = 0, target = 5;

    dijkstra_M(start, n, gm, vis, dis, pre);
    DFS(target, start, pre);

    printf("\n");

    dijkstra_L(start, n, gl, vis, dis, pre);
    DFS(target, start, pre);

    return 0;
}
```

### 图 - 单源路径模板 - Dijkstra+DFS <font color="red">❤</font>

> **!!! 默写过去** ；无向图记得要赋值双向，即v1->v2, v2->v1；

```c++
const int MAXN = 0x1ff;
const int INF = 0x3fffffff;

int Graph[MAXN][MAXN];
int Dis[MAXN];
bool Visit[MAXN];
vector<int> Pre[MAXN];
vector<vector<int> > Routes;


void dijkstra(int start, int n) {
    //初始化距离数组与访问数组
    fill(Dis, Dis+MAXN, INF);
    fill(Visit, Visit+MAXN, false);

    //设置起始点
    Dis[start] = 0;

    //至多循环n次
    int loop_time = n;
    while (loop_time--) {

        //找到未被访问过的点中，距离起点最近的点
        int minV = -1, minW = INF;
        for (int i=0; i<n; i++) {
            if (!Visit[i] && Dis[i]<minW) {
                minV = i;
                minW = Dis[i];
            }
        }
        if (minV == -1) break;
        else Visit[minV] = true;

        //更新与该点相连的点到起点的最短距离
        for (int i=0; i<n; i++) {
            if (!Visit[i] && Graph[minV][i]!=INF) {
                int td = Dis[minV] + Graph[minV][i];
                if (td < Dis[i]) {
                    Dis[i] = td;
                    Pre[i].clear();
                    Pre[i].push_back(minV);
                }
                else if (td == Dis[i]) {
                    Pre[i].push_back(minV);
                }
            }
        }
    }
}

//朴素遍历
void dfs(int v, vector<int> &store) {
    store.push_back(v);
    if (Pre[v].empty()) {
        Routes.push_back(store);
        //此处可以处理添加条件
    }
    else {
        for (int i=0; i<Pre[v].size(); i++) {
            dfs(Pre[v][i], store);
        }
    }
    store.pop_back();
}

int main() {
    int N, L;
    cin >> N >> L;

    //初试化图
    fill(Graph[0], Graph[0]+MAXN*MAXN, INF);
    while (L--) {
        int v1, v2, w;
        cin >> v1 >> v2 >> w;
        Graph[v1][v2] = w;
    }

    //求最短路径
    int S = 0, E = 3;
    dijkstra(S, N);

    //遍历
    vector<int> store;
    dfs(E, store);


    //输出
    cout << "\nMinimal distance from \"" << S << "\" to \"" << E << "\" is " << Dis[E] << "." << endl;
    cout << "Routes:  ";
    for (int i=0; i<Routes.size(); i++) {
        cout << i << ": ";
        for (int j=Routes[i].size()-1; j>0; cout << Routes[i][j] << "->", j--);
        cout << Routes[i][0] << " ;  ";
    }
    cout <<endl;

    return 0;
}
```

### 图 - 单源路径模板  - Bellman-Ford + DFS

```c++
const int MAXN = 0x3ff;
const int INF = 0x3fffffff;

struct node {
    int v; //结点
    int w; //边权

    node(){}
    node(int _v, int _w){
        v = _v;
        w = _w;
    }
};

vector<node> Edge[MAXN];
set<int> Pre[MAXN];
int Dis[MAXN];
vector<vector<int> > Routes;

bool bellman_ford(int start, int n) {
    //初始化
    fill(Dis, Dis+MAXN, INF);

    //设置起始点
    Dis[start] = 0;

    //至多遍历n-1次
    int loop_time = n - 1;
    while (loop_time--) {
        bool isChanged = false;
        //遍历所有边，进行松弛操作
        for (int i=0; i<n; i++) {
            for (int j=0; j< Edge[i].size(); j++) {
                node tv = Edge[i][j];
                if (Dis[i] + tv.w < Dis[tv.v]) {
                    Dis[tv.v] = Dis[i] + tv.w;
                    Pre[tv.v].clear();
                    Pre[tv.v].insert(i);
                    isChanged = true;
                }
                else if (Dis[i] + tv.w == Dis[tv.v]) {
                    Pre[tv.v].insert(i);
                }
            }
        }
        if (!isChanged) return true;
    }

    //遍历所有边，判断是否有负边
    for (int i=0; i<n; i++) {
        for (int j=0; j< Edge[i].size(); j++) {
            if (Dis[i] + Edge[i][j].w < Dis[j]) {
                return false;
            }
        }
    }
    return true;
}

void dfs(int v, vector<int> &store) {
    store.push_back(v);
    if (Pre[v].empty()) {
        Routes.push_back(store);
    }
    else {
        for (set<int>::iterator it=Pre[v].begin(); it!=Pre[v].end(); ++it) {
            dfs((*it), store);
        }
    }
    store.pop_back();
}


int main () {
    int N, M, C1, C2;
    cin >> N >> M >> C1 >> C2;

    //初试化图
    while (M--) {
        int v1, v2, w;
        cin >> v1 >> v2 >> w;
        Edge[v1].push_back(node(v2, w));
        Edge[v2].push_back(node(v1, w));
    }


    bool re = bellman_ford(C1, N);

    if (!re) {
        cout << "There are negative edges." << endl;
    }
    else {
        vector<int> store;
        dfs(C2, store);
        //输出
        cout << "Routes:  ";
        for (int i=0; i<Routes.size(); i++) {
            cout << i << ": ";
            for (int j=Routes[i].size()-1; j>0; cout << Routes[i][j] << "->", j--);
            cout << Routes[i][0] << " ;  ";
        }
        cout <<endl;
    }

    return 0;
}
```

### 图 - 单源路径模板  - SPFA + DFS <font color="red">❤</font>

> SPFA与Bellman-Ford都可以用来判断<u>是否存在源点可达的负环</u>。

```c++
const int MAXN = 0x3ff;
const int INF = 0x3fffffff;

struct node {
    int v; //结点
    int w; //边权

    node(){}
    node(int _v, int _w){
        v = _v;
        w = _w;
    }
};

vector<vector<int> > Routes;
vector<node> Edge[MAXN];
set<int> Pre[MAXN];
int Dis[MAXN];
bool InQnow[MAXN];
int JoinQtime[MAXN];

bool SPFA(int start, int n) {
    fill(Dis, Dis+n, INF);
    fill(InQnow, InQnow+n, false);
    fill(JoinQtime, JoinQtime+n, 0);

    Dis[start] = 0;

    queue<int> vqueue;
    vqueue.push(start);
    InQnow[start] = true;

    while(!vqueue.empty()) {
        int u = vqueue.front();
        vqueue.pop();
        InQnow[u] = false;

        for (int i=0; i<Edge[u].size(); i++) {
            int v = Edge[u][i].v;
            int w = Edge[u][i].w;
            if (Dis[u] + w < Dis[v]) {
                Dis[v] = Dis[u] + w;
                Pre[v].clear();
                Pre[v].insert(u);
                if (!InQnow[v]) {
                    vqueue.push(v);
                    InQnow[v] = true;
                    if ((++JoinQtime[v]) > n-1) { //有负环
                        return false;
                    }
                }
            }
            else if (Dis[u] + w == Dis[v]) {
                Pre[v].insert(u);
            }
        }
    }
    return true;
}

void dfs(int v, vector<int> &store) {
    store.push_back(v);
    if (Pre[v].empty()) {
        Routes.push_back(store);
    }
    else {
        for (set<int>::iterator it=Pre[v].begin(); it!=Pre[v].end(); ++it) {
            dfs((*it), store);
        }
    }
    store.pop_back();
}


int main () {
    int N, M, C1, C2;
    cin >> N >> M >> C1 >> C2;

    //初试化图
    while (M--) {
        int v1, v2, w;
        cin >> v1 >> v2 >> w;
        Edge[v1].push_back(node(v2, w));
        Edge[v2].push_back(node(v1, w));
    }


    bool re = SPFA(C1, N);

    if (!re) {
        cout << "There are negative edges." << endl;
    }
    else {
        vector<int> store;
        dfs(C2, store);
        //输出
        cout << "Routes:  ";
        for (int i=0; i<Routes.size(); i++) {
            cout << i << ": ";
            for (int j=Routes[i].size()-1; j>0; cout << Routes[i][j] << "->", j--);
            cout << Routes[i][0] << " ;  ";
        }
        cout <<endl;
    }

    return 0;
}

```

### 图 - 全源最短路径算法 - Floyd算法

> 允许有负权边，不允许有负权环

```c++
const int MAXN = 0x1ff;
const int INF = 0x3fffffff;

int Dis[MAXN][MAXN];
set<int> Path[MAXN][MAXN];
vector<vector<int> > Routes;

void floyd(int n) {
    for (int k=0; k<n; k++) {
        for (int i=0; i<n; i++) {
            for (int j=0; j<n; j++) {
//                if (Dis[i][k]!=INF && Dis[k][j]!=INF && Dis[i][k] + Dis[k][j] < Dis[i][j]) {
//                    Dis[i][j] = Dis[i][k] + Dis[k][j];
//                    Path[i][j] = k;
//                }
                if (Dis[i][k]!=INF && Dis[k][j]!=INF) {
                    if (Dis[i][k] + Dis[k][j] < Dis[i][j]) {
                        Dis[i][j] = Dis[i][k] + Dis[k][j];
                        Path[i][j].clear();
                        Path[i][j].insert(k);
                    }
                    else if (Dis[i][k] + Dis[k][j] == Dis[i][j]) {
                        Path[i][j].insert(k);
                    }
                }
            }
        }
    }
}

void getPath(int i, int j, int d, vector<int> &store) {
//    if (Path[i][j] == -1) {
//        store.push_back(j);
//    }
//    else {
//        int k = Path[i][j];
//        getPath(i, k, store);
//        getPath(k, j, store);
//    }
    if (j == d) { //如果到达终点，存储当前路径
        store.push_back(j);
        Routes.push_back(store);
        store.pop_back();
    }

    if (Path[i][j].empty()) { //如果i与j之间无中间点，则说明i直达j，即最短路径中包含j
        store.push_back(j);
    }
    else {
        for (set<int>::iterator it=Path[i][j].begin(); it!=Path[i][j].end(); ++it) {
            vector<int> t = store;
            getPath(i, (*it), d, store);
            getPath((*it), j, d, store);
            store = t;
        }
    }
}

int main() {
    int N, M, S, D;
    cin >> N >> M >> S >> D;

    fill(Dis[0], Dis[0]+MAXN*MAXN, INF);
//    fill(Path[0], Path[0]+MAXN*MAXN, -1);

    while (M--) {
        int v1, v2, d;
        cin >> v1 >> v2 >> d;
        Dis[v1][v2] = Dis[v2][v1] = d;
    }

    //计算全源最短路径
    floyd(N);

    //获取指定起点与终点的最短路径（可能有多条）
    vector<int> store;
    store.push_back(S);
    getPath(S, D, D, store);

    //输出
    cout << "Routes:  ";
    for (int i=0; i<Routes.size(); i++) {
        cout << i << ": ";
        int j = 0;
        for (; j<Routes[i].size()-1; cout << Routes[i][j] << "->", j++);
        cout << Routes[i][j] << " ;  ";
    }
    cout <<endl;

    return 0;
}
```

### 最小生成树 - kruskal算法

> “边”贪心的算法；

```c++
const int MAXN = 0x1ff;
const int INF = 0x3fffffff;


struct edge{
    int u, v; //边的两端
    int d; //边权

    edge() {}
    edge(int _u, int _v, int _d) {
        u = _u;
        v = _v;
        d = _d;
    }
};

bool cmp(edge a, edge b) {
    return a.d < b.d;
}

vector<edge> Edges;
int father[MAXN];

int findFather(int t) {
    int f = t;
    while (f!=father[f]) {
        f = father[f];
    }
    while (t!=father[t]) {
        int tt = t;
        t = father[t];
        father[tt] = f;
    }
    return f;
}

bool kruskal(int n, vector<edge> &store) {

    sort(Edges.begin(), Edges.end(), cmp);

    for (int i=0; i<n; father[i]=i ,i++);

    for (int i=0; i<Edges.size() && store.size()<n-1; i++) {
        edge e = Edges[i];
        int fu = findFather(e.u);
        int fv = findFather(e.v);
        if (fu != fv) {
            father[fu] = fv;
            store.push_back(Edges[i]);
        }
    }

    if (store.size()==n-1) return true;
    else return false;
}


int main() {
    int N, M;
    cin >> N >> M;

    while (M--) {
        int v1, v2, d;
        cin >> v1 >> v2 >> d;
        Edges.push_back(edge(v1, v2, d));
    }

    vector<edge> store;
    bool re = kruskal(N, store);

    if (re) {
        int totalD = 0;
        for (int i=0; i<store.size(); i++) {
            cout << store[i].u << "--" << store[i].v << endl;
            totalD += store[i].d;
        }
        cout << totalD << endl;
    }
    else {
        cout << "No answer!" << endl;
    }
    return 0;
}
```

### DAG 最长路径 - 动态规划算法

```c++
struct node {
    int v; int d;
    node(){}
    node(int _v, int _d) {v = _v; d = _d;}
};

vector<node> Edge[MAXN];

set<int> Next[MAXN];

int Dp[MAXN];

int dp_DAG(int u) {
    if (Dp[u] > 0) {
        return Dp[u];
    }
    else {
        for (int i=0; i<Edge[u].size(); i++) {
            int v = Edge[u][i].v;
            int d_uv = Edge[u][i].d;
            int temp = dp_DAG(v) + d_uv;
            if (temp > Dp[u]) {
                Dp[u] = temp;
                Next[u].clear();
                Next[u].insert(v);
            }
            else if (temp == Dp[u]) {
                Next[u].insert(v);
            }
        }
        return Dp[u];
    }
}

vector<vector<int> > Routes;

void dfs(int u, vector<int> &store) {
    store.push_back(u);
    if (Next[u].empty()) {
        Routes.push_back(store);
    }
    else {
        for (set<int>::iterator it=Next[u].begin(); it!=Next[u].end(); ++it) {
            dfs((*it), store);
        }
    }
    store.pop_back();
}


int main() {

    fill(Dp, Dp+MAXN, 0); //在不设置终点的情况下，可以初始化距离数组为0，作为递归边界
    dp_DAG(0);

    vector<int> store;
    dfs(0, store);

    
    return 0;
}
```

### DAG 最长路径（指定终点）

```c++
vector<node> Edge[MAXN];

set<int> Next[MAXN];

int Dp[MAXN];
bool Vis[MAXN];

int dp_DAG(int u) {
    if (Vis[u]) {
        return Dp[u];
    }
    else {
        Vis[u] = true;
        for (int i=0; i<Edge[u].size(); i++) {
            int v = Edge[u][i].v;
            int d_uv = Edge[u][i].d;
            int temp = dp_DAG(v) + d_uv;
            if (temp > Dp[u]) {
                Dp[u] = temp;
                Next[u].clear();
                Next[u].insert(v);
            }
            else if (temp == Dp[u]) {
                Next[u].insert(v);
            }
        }
        return Dp[u];
    }
}

int main() {

	fill(Dp, Dp+MAXN, -INF);
    fill(Vis, Vis+MAXN, false);
    int end_point = 4;
    Dp[end_point] = 0;
    Vis[end_point] = true;
    dp_DAG(0);

    vector<int> store;
    dfs(0, store);

    return 0;
}
```











------



## 题目

### PAT A1060 [判断长浮点数是否相等](https://pintia.cn/problem-sets/994805342720868352/problems/994805413520719872)

```c++
int n;

int handle(string &a) {
    int e;

    // 去除前导0
    int gcc;
    for (gcc=0; a[gcc]=='0'; gcc++);
    a.erase(0, gcc);

    // 0.00xxx 型
    if (a[0]=='.') {
        for (gcc=1; a[gcc]=='0'; gcc++);
        e = (gcc==a.size()) ? 0 : 1 - gcc;
        a.erase(0, gcc);
    }
    // xx.00x 型
    else {
        for (e=0;e<a.size();e++) {
            if (a[e]=='.') {
                a.erase(a.begin()+e);
                break;
            }
        }
    }
    if (a.size() > n) {a = a.substr(0, n);}
    else { for(int i=a.size(); i< n;i++,a=a+"0");}

    return e;
}

int main() {

    string a, b;
    cin >> n >> a >> b;

    int ea = handle(a);
    int eb = handle(b);

    if (ea==eb && a==b) {
        cout << "YES" << " 0." << a << "*10^" << ea << endl;
    }
    else {
        cout << "NO" << " 0." << a << "*10^" << ea << " 0." << b << "*10^" << eb << endl;
    }

    return 0;

}
```

### Codeup [简单计算器](http://codeup.cn/problem.php?cid=100000605&pid=0)

```c++
int main() {
    char in[256];

    while (gets(in)) {
        if (strlen(in)==1 && in[0]=='0') {
            break;
        }

        queue<double> nums;
        queue<char> ops;

        char *delim = " ";
        char *re;
        double num;
		
        // 拆分字符串
        re = strtok(in, delim);
        sscanf(re, "%lf", &num);
        nums.push(num);
        while ((re = strtok(NULL, delim)) != NULL) {
            if (isdigit(re[0])) {
                sscanf(re, "%lf", &num);
                nums.push(num);
            }
            else {
                ops.push(re[0]);
            }
        }

        stack<double> stackN;
        stack<char> stackO;

        double a, b;
        char op;

        stackN.push(nums.front()); nums.pop();

        while (!nums.empty()) {
            op = ops.front(); ops.pop();
            num = nums.front(); nums.pop();
            switch (op) {
                case '+': case '-':
                    if (!stackO.empty()) {
                        a = stackN.top(); stackN.pop();
                        b = stackN.top(); stackN.pop();
                        if (stackO.top()=='+') a=b+a;
                        else if (stackO.top()=='-') a=b-a;
                        stackO.pop();
                        stackN.push(a);
                    }
                    stackO.push(op);
                    stackN.push(num);
                    break;
                case '*':
                    b = stackN.top(); stackN.pop(); stackN.push(b * num);
                    break;
                case '/':
                    b = stackN.top(); stackN.pop(); stackN.push(b / num); 
                    break;
                default :
                    cout << "something wrong with op:" << op << endl;
            }
        }

        while (!stackO.empty()) {
            op = stackO.top(); stackO.pop();
            a = stackN.top(); stackN.pop();
            b = stackN.top(); stackN.pop();

            if (op=='+') { stackN.push(b+a); }
            else if (op=='-') { stackN.push(b-a); }
            else {cout << "something wrong with op: " << op << endl;}
        }
        printf("%.2f\n", stackN.top());
    }
    return 0;
}
```

### PAT A1032 [静态链表](https://pintia.cn/problem-sets/994805342720868352/problems/994805460652113920)

```c++
struct Node{
    char data;
    bool flag;
    int next;
}node[100000

int main() {
    int h1, h2, n;
    scanf("%d%d%d", &h1, &h2, &n);

    int addr, next;
    char data;
    for (int i=0; i<n; i++) {
        scanf("%d %c%d", &addr, &data, &next);
        node[addr].data = data;
        node[addr].next = next;
        node[addr].flag = false;
    }
    for (int i=h1; i != -1; node[i].flag=true, i=node[i].next);
    for (int i=h2; i != -1; i=node[i].next) {
        if (node[i].flag) {
            printf("%05d\n", i);
            return 0;
        }
    }
    printf("-1\n");
    return 0;
}
```

### 算法笔记 P273

```c++
const int TARGET = 6;
const int K = 2;
const vector<int> IN = {2, 3, 3, 4};
const int MAXN = IN.size();

void DFS(int index, int sum, int sumK, int sumS, vector<int> &sequence) {
    // 递归终结
    if (sum==TARGET && sumK==K) {
        for (vector<int>::iterator it=sequence.begin(); it!=sequence.end(); printf("%d ", IN[*(it)]), ++it);
        printf(" sumS = %d\n", sumS); return;
    }
    else if (sum>TARGET || sumK>K || index>=MAXN) {
        return;
    }

    // 选择当前值
    sequence.push_back(index);
    DFS(index+1, sum+IN[index], sumK+1, sumS+IN[index]*IN[index], sequence);
    sequence.pop_back();

    // 不选择当前值
    DFS(index+1, sum, sumK, sumS, sequence);
}

int main() {
    vector<int> seq;
    DFS(0, 0, 0, 0, seq);
    return 0;
}
```

### 算法笔记 P276 BFS与DFS的应用

```c++
const int MAXH = 6;
const int MAXL = 7;

int matrix[MAXH][MAXL] = {
    {0,1,1,1,0,0,1},
    {0,0,1,0,0,0,0},
    {1,0,0,0,1,0,0},
    {0,0,0,1,1,1,0},
    {1,1,1,0,1,0,0},
    {1,1,1,1,0,0,1}};

int X[] = {0, 0, 1, -1};
int Y[] = {1, -1, 0, 0};


struct node {
    int x;
    int y;

    node(){}
    node(int _x, int _y): x(_x), y(_y) {}
};

typedef struct node Node;

void BFS(int i, int j) {
    queue<node> nodes;
    matrix[i][j] = 0;
    Node t = node(i, j);
    nodes.push(t);
    while (!nodes.empty()) {
        Node v = nodes.front();
        nodes.pop();
        for (int k=0; k<4; k++) {
            int newx = v.x + X[k];
            int newy = v.y + Y[k];
            if ((newx<MAXH && newy<MAXL) && matrix[newx][newy]) {
                matrix[newx][newy] = 0;
                Node m = node(newx, newy);
                nodes.push(m);
            }
        }
    }
}

void DFS(int i, int j) {
    if (matrix[i][j]==0 || i>=MAXH || j>=MAXL) {
        return;
    }
    matrix[i][j] = 0;
    for (int k=0; k<4; k++) {
        int newx = i + X[k];
        int newy = j + Y[k];
        DFS(newx, newy);
    }
}

int main() {
    int gcc = 0;
    for (int i=0; i<MAXH; i++) {
        for (int j=0; j< MAXL; j++) {
            if (matrix[i][j]) {
                gcc++;
                BFS(i, j);
//                DFS(i, j);
            }
        }
    }

    printf("%d", gcc);
    return 0;
}
```

### PAT [A1034](https://pintia.cn/problem-sets/994805342720868352/problems/994805456881434624) 图的应用（DFS解法）

```c++
map<string, int> name2id;
map<int, string> id2name;
int Edges[2048][2048] = {0};
int Weights[2048] = {0};

int maxW, maxV;
int totalW;
set<int> totalV;

void DFS(int v) {
    if (Weights[v]>maxW) {
        maxV = v;
        maxW = Weights[v];
    }
    for (int i=0; i<name2id.size(); i++) {
        if (Edges[v][i]) {
            totalW += Edges[v][i];
            totalV.insert(i);
            Edges[v][i] = Edges[i][v] = 0;
            DFS(i);
        }
    }
}

int main() {
    int N, K;
    scanf("%d%d", &N, &K);

    int name_count = 0;
    for (int i=0; i<N; i++) {
        char t1[4], t2[4];
        int tw;
        scanf("%s%s%d", t1, t2, &tw);
        if (name2id.find(t1)==name2id.end()) {
            name2id.insert(pair<string, int>(t1, name_count));
            id2name.insert(pair<int, string>(name_count++, t1));
        }
        if (name2id.find(t2)==name2id.end()) {
            name2id.insert(pair<string, int>(t2, name_count));
            id2name.insert(pair<int, string>(name_count++, t2));
        }
        Edges[name2id[t1]][name2id[t2]] += tw;
        Edges[name2id[t2]][name2id[t1]] += tw;
        Weights[name2id[t1]] += tw;
        Weights[name2id[t2]] += tw;
    }

    map<string, int> bosses;

    for (int i=0; i<name2id.size(); i++) {
        totalV.clear();
        totalV.insert(i);
        totalW = 0;
        maxV = i;
        maxW = Weights[i];
        DFS(i);
        if (totalV.size() > 2 && totalW > K) {
            bosses.insert(pair<string, int>(id2name[maxV], totalV.size()));
        }
    }

    cout << bosses.size() << endl;
    for (map<string, int>::iterator it=bosses.begin(); it!=bosses.end(); ++it) {
        cout << it->first << " " << it->second << endl;
    }

    return 0;
}
```

### PAT [A1034](https://pintia.cn/problem-sets/994805342720868352/problems/994805456881434624) 图的应用（并查集解法）

```c++
const int MAXN = 2048;

map<string, int> name2id;
map<int, string> id2name;

int Weights[MAXN] = {0};

int Father[MAXN];

int find_UFS(int a) {
    int f = a;
    while (f != Father[f]) {
        f = Father[f];
    }

    while (a != Father[a]) {
        int t = a;
        a = Father[a];
        Father[t] = f;
    }
    return f;
}

void union_UFS(int a, int b) { 
    int fa = find_UFS(a);	// 易错点！
    int fb = find_UFS(b);
    if (Weights[fa] > Weights[fb]) {
        Father[fb] = fa;
    }
    else {
        Father[fa] = fb;
    }
}

struct node {
    int totalV;
    int totalW;

    node (){}
    node(int _v, int _w) {
        totalV = _v;
        totalW = _w;
    }
};

int main() {

    int N, K;
    scanf("%d%d", &N, &K);

    for (int i=0; i<MAXN; Father[i] = i, i++);

    int name_count = 0;
    vector<pair<int, int> > input_memory;
    for (int i=0; i<N; i++) {
        string t1, t2;
        int tw;
        cin >> t1 >> t2 >> tw;
        if (name2id.find(t1)==name2id.end()) {
            name2id[t1] = name_count;
            id2name[name_count++] = t1;
        }
        if (name2id.find(t2)==name2id.end()) {
            name2id[t2] = name_count;
            id2name[name_count++] = t2;
        }
        Weights[name2id[t1]] += tw;
        Weights[name2id[t2]] += tw;

        input_memory.push_back(pair<int,int>(name2id[t1], name2id[t2]));
    }

    for (int i=0; i<N; i++) {
        union_UFS(input_memory[i].first, input_memory[i].second);
    }

    map<int, node> nodes;
    for (int i=0; i<name_count; i++) {
        int f = find_UFS(i);
        if (nodes.find(f) == nodes.end()) {
            nodes[f] = node(1, Weights[i]);
        }
        else {
            nodes[f].totalV += 1;
            nodes[f].totalW += Weights[i];
        }
    }

    map<string, int> outputs;
    for (map<int, node>::iterator it=nodes.begin(); it!=nodes.end(); ++it) {
        if (it->second.totalV > 2 && it->second.totalW > 2*K) {
            outputs[id2name[it->first]] = it->second.totalV;
        }
    }

    cout << outputs.size() << endl;
    for (map<string, int>::iterator it=outputs.begin(); it!=outputs.end(); ++it) {
        cout << it->first << " " << it->second << endl;
    }
    return 0;
}
```

### PAT [A1076](https://pintia.cn/problem-sets/994805342720868352/problems/994805392092020736) 图相关 BFS

```c++
struct node { // 使用邻接表进行存储时，边权、层数等信息需要使用结构体存储
    int vertex;
    int level;

    node(){}
    node(int _v, int _l) {
        vertex = _v;
        level = _l;
    }
};

const int MAXN = 1024;
vector<int> Edges[MAXN];

int main() {
    int N, L;
    scanf("%d%d", &N, &L);
    for (int i=1; i<=N; i++) {
        int tcount;
        scanf("%d", &tcount);
        for (int j=0; j<tcount; j++) {
            int tnum;
            scanf("%d", &tnum);
            Edges[tnum].push_back(i);
        }
    }
    int tN;
    scanf("%d", &tN);
    while (tN--) {
        int target;
        queue<node> qnode;
        bool InQueue[MAXN] = {false};

        scanf("%d", &target);
        qnode.push(node(target, 1));
        InQueue[target] = true;

        int tran_count = 0;
        while (!qnode.empty()) { // BFS遍历
            node tn = qnode.front();
            qnode.pop();
            if (tn.level > L) continue;
            for (int i=0; i<Edges[tn.vertex].size(); i++) {
                int tv = Edges[tn.vertex][i];
                if (!InQueue[tv]) {
                    qnode.push(node(tv, tn.level+1));
                    InQueue[tv] = true;
                    tran_count += 1;
                }
            }
        }
        printf("%d\n", tran_count);
    }
    return 0;
}
```

### PAT [数字黑洞](https://pintia.cn/problem-sets/994805260223102976/problems/994805302786899968)

```c++
bool cmp1(char a, char b) {
    return a-b >0;
}

bool cmp2(char a, char b) {
    return a-b<0;
}

int main() {

    char input[5];
    int re;

    scanf("%d", &re);

    int tmax, tmin;

    do {
        sprintf(input, "%04d", re);

        sort(input, input+4, cmp1);

        sscanf(input, "%d", &tmax);

        sort(input, input+4, cmp2);

        sscanf(input, "%d", &tmin);

        re = tmax - tmin;

        printf("%04d - %04d = %04d\n", tmax, tmin, re);
    } while (re != 6174 && re!=0);

    return 0;
}
```




#### `push_back`和`emplace_back`的差别

vector中`push_back`和`emplace_back`差别：

同样是在容器尾部追加一个元素，但`emplace_back`在效率上要比`push_back`好，原因是`push_back`完成这个任务的过程是：先构造一个临时对象，然后调用移动构造函数将这个临时对象的副本拷贝到容器末尾增加的元素中，最后调用析构函数释放掉临时对象；而`emplace_back`完成这个任务的过程是：直接使用构造函数在容器末尾增加一个元素。`emplace_back`比`push_back`少了一次对象的构造和析构，因此`emplace_back`更高效。

不过相比于`push_back`，`emplace_back`的缺点是代码可读性相对较差。因此，对于往容器尾部添加元素的操作，选择`push_back`会使代码可读性更好，代码更健壮。

```c++
#include<iostream>
#include <vector>
using namespace std;

class MyTest
{
public:
    //普通构造
    MyTest(int id,int age):m_id(id),m_age(age)
    { 
        cout << "ceate MyTest class..." << this << endl;
    }
    //拷贝构造
    MyTest(const MyTest &t):m_id(t.m_id),m_age(t.m_age)
    {  
        cout << "copy construct called..." << this << endl;
    }
    //移动构造
    MyTest(const MyTest &&t)
    {
        m_id = std::move(t.m_id);
        m_age = std::move(t.m_age);
        cout << "move contruct called.." << this << endl;
    }
    //析构
    ~MyTest()
    {
        cout << "destory MyTest class..." << this << endl;
    }
private:
    int m_id; //id成员
    int m_age;//age成员
};

int main(int argc, char *argv[])
{
    vector<MyTest> vec;
    vec.reserve(2);  //预先分配内存
    cout << "\n ------ push_back --------" << endl;
    vec.push_back(MyTest(1,20));
    cout << "\n ------ emplace_back --------" << endl;
    vec.emplace_back(1,20);
    cout << "\n -------- finish -------- " << endl;
}

//output g++ -g -Wall -std=c++11 -o test test.cpp
 ------ push_back --------
ceate MyTest class...
move contruct called..
destory MyTest class...

 ------ emplace_back --------
ceate MyTest class...

 -------- finish --------
destory MyTest class...
destory MyTest class...
```



#### `unordered_set`

`unordered_set`是一种**关联容器**，set和map内部实现是基于**RB-Tree**，是有序的，`unordered_set`和`unordered_map`是基于**hash table**。是无序的。

这种容器不能存放重复的元素。元素类型必须可以比较是否相等，因为这可以确定元素什么时候相等。就像 `unordered_map`，元素被存放在哈希表内部的格子中。每个格子保存哪个元素，是由元素的哈希值决定的。`unordered_set `容器组织方式的概念图如下所示：

![img](http://m.biancheng.net/uploads/allimg/180918/2-1P91Q02449C2.jpg)

**定义**

`unordered_set<int> hash;`

**操作**

`hash.size()`元素个数

`hash.empty()`

`hash.max_size()`获取最大容量值

**迭代器操作**

`unordered_set<int>::iterator it;`

`unordered_set<int>::iterator ite_begin=c1.begin();`//返回头迭代器

`unordered_set<int>::iterator ite_end=c1.end();` //返回尾部迭代器

```c++
**//槽迭代器**
unordered_set<int>::iterator local_iter_begin=c1.begin(1);
unordered_set<int>::iterator local_iter_end=c1.end(1);
```

**基本操作**

`find()`通过给定的主键查找元素` unordered*set<int>::iterator find*iterator = hash.find(1);`

`count()`返回匹配给定主键元素的个数` hash.count(1);`

`insert()`插入函数 `hash.insert(1);`

`erase()`删除`hash.erase(1);`

`clear()`清空`hash.clear();`

`swap()`交换 `hash.swap(hash2);`



**内存操作**

`hash.rehash(10)`//设置槽位数

`hash.reserve(1000)`//改变容器的容量



#### 数组或者vector求最大最小值

`vector<int> v;`

- 求最大值 `int maxValue = *max_element(v.begin(), v.end());`
- 求最小值`int maxValue = *min_element(v.begin(), v.end());`
- 求最大值坐标 `int maxPosition = max_element(v.begin(), v.end()) - v.begin()`
- 求最大值坐标 `int minPosition = min_element(v.begin(), v.end()) - v.begin()`



#### vector求和

```c++
vector<int> v;

int ret = accumulate(v.begin(), v.end(), 0);
```

accumulate 函数第三个参数初值　赋值的时候一定要注意 所累加的vector的类型，如果vector是float或者double型, 赋值的时候如果给０，而不是0.0，那么就会出现累加的小于１的数都是０；因此如果是float或double类型的vector，使用accumulate时第三个参数应为0.0，否则就会出错。


#### STL反向排序

我们假定一个序列是正序的：

对于数值型，从小到大
对于字符串，字典序
对于类类型，需自定义
这里我以数值型反向排序为例说明：

方法1：sort增加谓词

```c++
vector<int> ivec{1,3,5,2,6,7,4,9};
sort(ivec.begin(),ivec.end(),[](int a,int b){return a>b;});
```

方法2：反向迭代器

```c++
vector<int> ivec{1,3,5,2,6,7,4,9};
sort(ivec.rbegin(),ivec.rend());
```

方法3：sort后再反序

```c++
vector<int> ivec{1,3,5,2,6,7,4,9};
sort(ivec.begin(),ivec.end());
reverse(ivec.begin(),ivec.end());
```






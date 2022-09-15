**stringstream**是C++提供的一个字符串流（stream），用于字符串和其他类型的转换。

在C语言中，常用的字符串和数字转换函数是sscan和sprintf函数。

常见格式串：

- %% 印出百分比符号，不转换。
- %c 整数转成对应的 ASCII 字元。
- %d 整数转成十进位。
- %f 倍精确度数字转成浮点数。
- %o 整数转成八进位。
- %s 整数转成[字符串](https://so.csdn.net/so/search?q=字符串&spm=1001.2101.3001.7020)。
- %x 整数转成小写十六进位。
- %X 整数转成大写十六进位。
- %n `sscanf(str, "%d%n", &dig, &n)`，%n表示一共转换了多少位的字符



##### `sprintf`函数

`sprintf`函数原型为`int sprintf(char *str, const char *format, ...)`。作用是格式化字符串，具体功能如下：

1. 将数字变量转化成字符串。
2. 得到整型变量的16进制和8进制字符串。
3. 连结多个字符串。

```c++
int main(){
    char str[256] = { 0 };
    int data = 1024;
    //将data转换为字符串
    sprintf(str,"%d",data);
    //获取data的十六进制
    sprintf(str,"0x%X",data);
    //获取data的八进制
    sprintf(str,"0%o",data);
    const char *s1 = "Hello";
    const char *s2 = "World";
    //连接字符串s1和s2
    sprintf(str,"%s %s",s1,s2);
    cout<<str<<endl; 
    return 0;
} 
```



##### `sscanf`函数

`sscanf`函数的原型为`int sscanf(const char*, const char *format, ...)`。将参数str的字符串根据参数format字符串来转换并格式化数据，转换后的结果存于对应的参数内。具体功能如下：

1. 根据格式从字符串中提取数据，如从字符串中取出整数，浮点数和字符串等。
2. 取指定长度的字符串。
3. 取到指定字符为止的字符串。
4. 取仅包含指定字符集为止的字符。
5. 取到指定字符集为止的字符串。

```c++
int main(){
    char s[15] = "123.432,432";
    int n;
    double f1;
    int f2;
    sscanf(s, "%lf,%d%n", &f1, &f2, &n);
    cout<<f1<<" "<<f2<<" "<<n;
    return 0;
} 
```



##### `stringstream`类

`stringstream`是C++提供的一个字符串流，要使用stringstream，必须包含其头文件：

```cpp
#include<sstream>
using namespace std;
stringstream ss;
```

< sstream > 库定义了三种类：istringstream、ostringstream和stringstream，分别用来进行流的输入、输出和输入输出操作。另外，每个类都有一个对应的宽字符集版本。一般情况下使用stringstream就足够，因为字符串要频繁的涉及到输入输出。

< sstream > 使用string对象来代替字符数组，这样可以避免缓冲区溢出的危险。而且，传入参数和目标对象的类型被自动推导出来，即便使用了不正确的格式化符也没有危险。

与文件流fstream类似，通过插入器(<<)和析取器(>>)这两个运算符可以直接对`stringstream`上的数据输入输出，而将stringstream中的全部数据输出则是使用成员函数str()，其有两种形式：

- `void str()` //无参形式，用于将`stringstream`流中的数据以string字符串的形式输出
- `void str (const string& s)`//以字符串为参数，用以覆盖`stringstream`流中的数据



###### `ss.clear()`成员函数

在对同一个stringstream对象重复赋值，就需要先对流使用clear()函数清空流的状态，此时流占用的内存没有改变，会一直增加(stringstream不主动释放内存)，若想改变内存(一般是清除内存，减少内存消耗)，需要再配合使用`str("")`清空stringstream的缓存。

清空 stringstream 有两种方法：`clear()` 方法以及 `str("")` 方法。如果想清空 stringstream，使用 `str("")` 的方式；`clear()` 方法适用于进行多次数据类型转换的场景。

```cpp

stringstream stream;
    int a,b;
    ss<<"80";//向流输出数据(写入)
    ss>>a;//从流输入数据到a
    cout<<"Size of ss = "<<ss.str().length()<<endl;//ss.str()返回一个string对象，再调用其成员函数length()
    ss.clear();//清空流
    ss.str("");//清空流缓存
    cout<<"Size of ss = "<<ss.str().length()<<endl;
    ss<<"90";//重新赋值
    ss>>b;
    cout<<"Size of ss = "<<ss.str().length()<<endl; 

/*
Size of ss = 2
Size of ss = 0
Size of ss = 2
80
90
*/
```

**stringstream通常是用来做数据转换的**，用于字符串与其他变量类型的转换，相比c库的转换，它更加安全，自动和直接。

```cpp
#include<iostream>  
#include<sstream>       
#include<string>  
using namespace std;
int main() 
{
	string str = "My name is 123";
	stringstream word(str);//或者stringstream word;word<<str;
	string a,b,c;
    int d;
	word >> a >> b >> c >> d;
	cout << a << endl << b << endl << c << endl << d << endl;
        return 0;
}
/*
My
name
is
123
*/
```



###### 多个字符串拼接

​    在 stringstream 中存放多个字符串，实现多个字符串拼接的目的（其实完全可以使用 string 类实现）：

```cpp

#include <sstream>
#include <iostream>
 
int main()
{
	std::stringstream sstream;
 
	// 将多个字符串放入 sstream 中
	sstream << "first" << " " << "string,";
	sstream << " second string";
 
    // 使用 str() 方法，可以将 stringstream 类型转换为 string 类型；
	std::cout << "strResult is: " << sstream.str() << std::endl;     // strResult is: first string, second string
 
    return 0;
}
```
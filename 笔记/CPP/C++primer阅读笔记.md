- 想要输出十进制（默认）、八进制和十六进制的数字时，分别使用dec、oct和hex，这些都位于标准库iostream中。

```c++
cout << oct;
cout << 42；
//52
cout << hex;
cout << 42 <<endl;
//2a
```



- cctype软件包

  ```c++
  #include<cctype>
  ```

  | 函数名称   |                                                    |
  | ---------- | -------------------------------------------------- |
  | isalpha()  | 参数是否是字母                                     |
  | isalnum()  | 参数是否是字母或数字                               |
  | isdigit()  | 参数是否为数字                                     |
  | islower()  | 是否是小写字母                                     |
  | iscntrl()  | 是否是控制字符                                     |
  | ispunct()  | 是否是标点符号                                     |
  | issupper() | 是否为大写字母                                     |
  | isspace()  | 是否为标准空白字符，如空格、进制、换行符、制表符等 |
  | tolower()  | 返回小写字母                                       |
  | toupper()  | 返回大写字母                                       |
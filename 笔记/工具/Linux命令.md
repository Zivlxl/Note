### mkdir

参数为-p 代表创建多级目录

```
mkdir -p aaa/bbb
```

### Vim

set nu 显示行号

#### 文件多开

sp hello.c 在文件下方打开一个新的文件hello.c

vsplit hello.c 在文件右边打开一个新的文件hello.c

打开一个文件后，命令模式下输入e file，打开另一个文件

文件间的切换：

- :bn    //下一个文件
- :bp    //上一个文件
- :ls    //列出打开的文件，带编号
- :b1~n  //切换至第n个文件
- Ctrl+6 //两文件间的切换

对于用(v)split在多个窗格中打开的文件，这种方法只会在当前窗格中切换不同的文件。

——————————————————————————————

### 压缩

#### .zip文件

##### zip

1. zip -r myfile.zip ./*
   将当前目录下的所有文件和文件夹全部压缩成myfile.zip文件,－r表示递归压缩子目录下所有文件.
2. zip -d myfile.zip smart.txt
   删除压缩文件中smart.txt文件
3. zip -m myfile.zip ./rpm_info.txt
   向压缩文件中myfile.zip中添加rpm_info.txt文件

##### unzip

1. unzip yasuo.zip

2. unzip -v large.zip

   不解压缩，查看文件

3. unzip -t large.zip

   验证一下这个压缩文件是否下载完全

4. unzip -j music.zip

   我用-v选项发现music.zip压缩文件里面有很多目录和子目录，并且子目录中其实都是歌曲mp3文件，我想把这些文件都下载到第一级目录，而不是一层一层建目录

#### .gz文件

##### gzip

1. gzip file1

   压缩文件

2. gzip -r file.gz file1 file2 dir/

   -r表示递归压缩

3. gzip -dv file.gz

   解压，-d表示解压，-v表示显示文件名和压缩比

4. gzip -l file.gz

   显示压缩包的内容

5. gzip -t 

   检测文件完整性

6. gzip -num file

    用指定的数字 num 调整压缩的速度，-1 或 –fast 表示最快压缩方法（低压缩比），-9 或 –best 表示最慢压缩方法（高压缩比）系统缺省值为 6

#### .bz2

##### bzip2

bzip2和gzip基本相同

1. bzip2 -k file

   保留原文件压缩

##### bunzip2

语法：bunzip2 [-fkLsvV].bz2压缩文件

参数：

- -f或--force 　解压缩时，若输出的文件与现有文件同名时，预设不会覆盖现有的文件。若要覆盖，请使用此参数。
- -k或--keep 　在解压缩后，预设会删除原来的压缩文件。若要保留压缩文件，请使用此参数。
- -s或--small 　降低程序执行时，内存的使用量。
- -v或--verbose 　解压缩文件时，显示详细的信息。
- -L,--license,-V或--version 　显示版本信息。

#### .Z

compress/uncompress

#### .tar.*

**1．**命令格式：

tar[必要参数][选择参数][文件] 

**2**．命令功能：

用来压缩和解压文件。tar本身不具有压缩功能。他是调用压缩功能实现的 

**3．**命令参数：

必要参数有如下：

-A 新增压缩文件到已存在的压缩

-B 设置区块大小

-c 建立新的压缩文件

-d 记录文件的差别

-r 添加文件到已经压缩的文件

-u 添加改变了和现有的文件到已经存在的压缩文件

-x 从压缩的文件中提取文件

-t 显示压缩文件的内容

-z 支持gzip解压文件

-j 支持bzip2解压文件

-Z 支持compress解压文件

-v 显示操作过程

-l 文件系统边界设置

-k 保留原有文件不覆盖

-m 保留文件不被覆盖

-W 确认压缩文件的正确性

可选参数如下：

-b 设置区块数目

-C 切换到指定目录

-f 指定压缩文件

--help 显示帮助信息

--version 显示版本信息

##### .tar

压缩：tar -cvf file.tar file1 file2

解压：tar -xvf 

##### .tar.gz

压缩：tar -zcvf file.tar.gz file1 file2

解压：tar -zxvf file.tar.gz

##### .tar.bz2/bz

压缩：tar -jcvf file.tar.bz2 file1 file2

解压：tar -jxvf file.tar.bz2

##### .tar.Z

压缩：tar -Zcvf file.tar.Z file1 file2

解压：tar -Zxvf file.tar.Z

——————————————————————————————

### WC

统计文件中的字节数、字数、行数

- -c 统计字节数
- -l 统计行数
- -m 统计字符数
- -w 统计字数

——————————————————————————————

### 查看文件夹下文件的数量

1. 查看当前文件夹中文件数量

   ls -l | grep "^-" | wc -l

2. 查看当前文件夹中文件数量，包含子目录中的文件

   ls -lR | grep "^-" | wc -l

3. 统计当前目录中文件夹的数量

   ls -l | grep "^d" | wc -l

4. 统计当前目录中文件夹的数量，包含子目录中文件夹

   ls -lR |grep "^d" | wc -l

5. 过滤查询

   ls -lR *.py | grep "^-" | wc -l

